### 部署记录

#### 2025-02-14

1、实现向量化前的分割文档。

终于解决了这个困扰好几天的事情。

之前在课程「2025004Building-Agentic-RAG-with-Llamaindex」中看到 Llamaindex 向量化之前用专门的分割器分割文档的。

```py
    # load documents
    documents = SimpleDirectoryReader(input_files=[file_path]).load_data()
    splitter = SentenceSplitter(chunk_size=1024)
    nodes = splitter.get_nodes_from_documents(documents)
    vector_index = VectorStoreIndex(nodes)
```

但是切换为用 weaviate 后，这个实现始终没成功，一度以为向量数据库不支持这种形式。weaviate 的向量化采用下面的形式实现的。只能整个 documents 向量化而不是切块向量化。而且还弄错：以为 batch_size 是之前切换的 chunk_size，这两个不是一个东西。batch_size 是处理的时候并发处理包的数量。

```py
def create_document_index(input_files, index_name):
    # 连接本地 Weaviate
    client = weaviate.connect_to_local()
    # 创建集合
    documents = client.collections.create(name=index_name)
    print("documents collection has been created.")
    # load documents
    documents = SimpleDirectoryReader(input_files=input_files).load_data()

    custom_batch = client.batch.fixed_size(
        batch_size=123,
        concurrent_requests=3,
        consistency_level=ConsistencyLevel.ALL,
    )
    vector_store = WeaviateVectorStore(
        weaviate_client=client,
        index_name=index_name,
        # we pass our custom batch as a client_kwargs
        client_kwargs={"custom_batch": custom_batch},
    )

    storage_context = StorageContext.from_defaults(vector_store=vector_store)
    index = VectorStoreIndex.from_documents(
        documents, storage_context=storage_context
    )

    print("All vector data has been written to Weaviate.")

    client.close()  # Free up resources
```

先切割文档再向量化的实现如下：

```py
def create_document_index(input_files, index_name, chunk_size=1024, chunk_overlap=200):
    try:
        # 连接本地 Weaviate
        client = weaviate.connect_to_local()

        # 检查集合是否存在，如果存在则删除
        if client.collections.exists(index_name):
            client.collections.delete(index_name)
            print(f"Existing collection {index_name} has been deleted.")
        
        # 创建集合
        documents = client.collections.create(name=index_name)
        print("documents collection has been created.")

        # load documents
        documents = SimpleDirectoryReader(input_files=input_files).load_data()
        # 设置文档分割器
        splitter = SentenceSplitter(chunk_size=chunk_size, chunk_overlap=chunk_overlap)
        nodes = splitter.get_nodes_from_documents(documents)

        vector_store = WeaviateVectorStore(
            weaviate_client=client,
            index_name=index_name,
        )

        storage_context = StorageContext.from_defaults(vector_store=vector_store)

        index = VectorStoreIndex(
            nodes,
            storage_context=storage_context,
            show_progress=True
        )

        print("All vector data has been written to Weaviate.")

    except Exception as e:
        print(f"Error occurred: {str(e)}")
        raise
    finally:
        if 'client' in locals():
            client.close()  # Ensure client is always closed
            print("Weaviate connection closed.")
```


#### 2025-02-13

1、增加向量数据库。

[Locally hosted | Weaviate](https://weaviate.io/developers/weaviate/quickstart/local)

开始仅仅看的官方文档，走了不少弯路。知道看了 llama_index 的官方文档才算解决。

[Weaviate Vector Store - LlamaIndex](https://docs.llamaindex.ai/en/stable/examples/vector_stores/WeaviateIndexDemo/)

本地部署向量数据库的基本思路：

01 docker 里部署向量数据库。

直接用官网提供的 `docker-compose.yml` 文件。配置文件里部署的时候可以在 weaviate 里配套指定嵌入模型和生成生成模型，也可以取消。这个地方给自己挖了坑。以为 weaviate 里只能在这里配置大模型。而 weaviate 配套的大模型只支持 openAI、Claude、Google 那些主流，没国内以及第三方平台的。后面卡在了这里，不知道如何跟之前 llama_index 里调用大模型连起来。

02 项目数据库里新建数据集。

```py
def create_document_collection():
    # 连接本地 Weaviate
    client = weaviate.connect_to_local()
    
    # 创建集合
    documents = client.collections.create(
        name="LlamaIndex",
        vectorizer_config=Configure.Vectorizer.text2vec_ollama(
            api_endpoint="http://host.docker.internal:11434",
            model="bge-m3:latest",
        ),
        generative_config=Configure.Generative.ollama(
            api_endpoint="http://host.docker.internal:11434",
            model="deepseek-r1:14b",
        )
    )

    client.close()  # Free up resources
```

这里其实嵌入模型和生成模型也不用指定的。模型都是用的外部的。

03 向量化数据存入数据库。

这就开始了坑点，开始用的官方思路储存的。

```py
def import_document_to_weaviate():
    # load documents
    documents = SimpleDirectoryReader(input_files=["../data/papers/metagpt.pdf"]).load_data()

    splitter = SentenceSplitter(chunk_size=1024)
    nodes = splitter.get_nodes_from_documents(documents)
    
    # 连接本地 Weaviate
    client = weaviate.connect_to_local()

    documents = client.collections.get("DocumentRAG")

    with documents.batch.dynamic() as batch:
        for node in nodes:
            text = node.get_content()
            metadata = node.get_metadata_str()
            batch.add_object({
                "content": text,
                "metadata": metadata,
            })
            if batch.number_errors > 10:
                print("Batch import stopped due to excessive errors.")
                break

    failed_objects = documents.batch.failed_objects
    if failed_objects:
        print(f"Number of failed imports: {len(failed_objects)}")
        print(f"First failed object: {failed_objects[0]}")

    client.close()  # Free up resources

    print("All vector data has been written to Weaviate.")
```

正确的应该是用 llama_index 官方文档提供的方法：

```py
def import_vector_document():
    # 连接本地 Weaviate
    client = weaviate.connect_to_local()

    # load documents
    documents = SimpleDirectoryReader(input_files=["../data/papers/metagpt.pdf"]).load_data()

    custom_batch = client.batch.fixed_size(
        batch_size=1024,
        concurrent_requests=4,
        consistency_level=ConsistencyLevel.ALL,
    )
    vector_store = WeaviateVectorStore(
        weaviate_client=client,
        index_name="LlamaIndex",
        # we pass our custom batch as a client_kwargs
        client_kwargs={"custom_batch": custom_batch},
    )

    storage_context = StorageContext.from_defaults(vector_store=vector_store)
    index = VectorStoreIndex.from_documents(
        documents, storage_context=storage_context
    )

    print("All vector data has been written to Weaviate.")

    client.close()  # Free up resources
```

04 从向量数据库中查询。

这里使用 llama_index 官方文档提供的方法，就可以跟课程「2025004Building-Agentic-RAG-with-Llamaindex」里的内容接上了。

```py
    # 连接本地 Weaviate
    client = weaviate.connect_to_local()

    vector_store = WeaviateVectorStore(
        weaviate_client=client, 
        index_name="LlamaIndex"
    )

    vector_index = VectorStoreIndex.from_vector_store(vector_store)

    vector_query_engine = vector_index.as_query_engine()

    vector_tool = QueryEngineTool.from_defaults(
        query_engine=vector_query_engine,
        description=(
            "Useful for retrieving specific context from the MetaGPT paper."
        ),
    )

    query_engine = RouterQueryEngine(
        selector=LLMSingleSelector.from_defaults(),
        query_engine_tools=[
            vector_tool,
        ],
        verbose=True
    )

    response = query_engine.query("What is the summary of the document?")
    print(str(response))
    print(len(response.source_nodes))

    response = query_engine.query("How do agents share information with other agents?")
    print(len(response.source_nodes))
    print(str(response))

    client.close()  # Free up resources
```




#### 2025-02-12

1、嵌入模型更换为本地。

from llama_index.core.embeddings import resolve_embed_model

Settings.embed_model = resolve_embed_model("local:/Users/Daglas/dalong.modelsets/bge-m3")


---

o3-mini-high 联网搜的解决方案

方法二：使用 LlamaIndex 提供的本地模型加载方式
如果您的 bge-m3 模型是通过 Ollama 部署在本地，并且需要以“本地嵌入模型”的方式加载（即不走 OpenAIEmbedding 类），可以采用 LlamaIndex 中的 resolve_embed_model 方法来加载本地模型。例如（注意：下面的路径仅供示例，您需要根据实际部署情况调整）：

python
复制
from llama_index.core.embeddings import resolve_embed_model

\# 例如，本地部署时您将 bge-m3 模型存放在某个目录下，
\# 或者通过 Ollama 的内部协议调用，构造对应的模型字符串（此处“local:”仅为标识，具体格式请参考您使用的 LlamaIndex 版本文档）
Settings.embed_model = resolve_embed_model("local:/path/to/your/bge-m3:latest")


2、增加 Google 的 gemini 大模型。

from llama_index.llms.gemini import Gemini

os.environ["http_proxy"] = "http://127.0.0.1:7890"
os.environ["https_proxy"] = "http://127.0.0.1:7890"

api_key = get_api_key()

model_name = "models/gemini-2.0-flash-exp"
Settings.llm = Gemini(
    api_key=api_key,
    model_name=model_name
)

---

o3-mini-high 联网搜的解决方案

在 llama_index 中调用 Google 的 Gemini 大模型，你可以使用 llama_index 内置的 Gemini 接口来完成。基本流程如下：

1. **安装相关包**  
   为了使用 Gemini 模型，需要安装支持 Gemini 的扩展包。例如：
   ```bash
   pip install llama-index-llms-gemini
   pip install llama-index-embeddings-gemini
   ```
   这些包会扩展 llama_index，使其支持调用 Google 的 Gemini 大模型。

2. **设置 Google API 密钥**  
   Gemini 模型需要一个有效的 Google API 密钥。你可以通过环境变量来配置密钥，例如：
   ```python
   import os
   os.environ["GOOGLE_API_KEY"] = "your_google_api_key"
   ```
   或者使用 getpass 等方式安全地获取密钥。

3. **初始化 Gemini 模型与嵌入模型**  
   在 llama_index 中，默认使用 Settings 对象来管理全局的 LLM 和嵌入模型。你可以将 Gemini 模型和 Gemini 嵌入模型分别设置给 Settings.llm 和 Settings.embed_model。例如：
   ```python
   from llama_index.llms.gemini import Gemini
   from llama_index.embeddings.gemini import GeminiEmbedding
   from llama_index import Settings

   # 设置 Gemini 嵌入模型（此处模型名称通常为 "models/embedding-001"，你也可以根据需要选择其他型号）
   Settings.embed_model = GeminiEmbedding(model_name="models/embedding-001", api_key=os.environ["GOOGLE_API_KEY"])
   
   # 初始化 Gemini LLM（如果需要指定更高版本的 Gemini，比如 gemini-1.5-pro-latest，也可在初始化时传入 model_name 参数）
   Settings.llm = Gemini(api_key=os.environ["GOOGLE_API_KEY"])
   ```
   这样全局的 LLM 与嵌入模型就配置好了，后续在构建索引或查询时会自动使用这两个设置。

4. **构建索引并发起查询**  
   以一个简单的示例来看，假设你有一个存放文档的文件夹（如 "data"），你可以用 SimpleDirectoryReader 加载文档，然后构建 VectorStoreIndex 并使用 Gemini LLM 进行查询：
   ```python
   from llama_index import SimpleDirectoryReader, VectorStoreIndex

   # 加载文档
   documents = SimpleDirectoryReader("data").load_data()

   # 从文档构建索引（内部会调用前面设置好的 Gemini 嵌入模型）
   index = VectorStoreIndex.from_documents(documents)

   # 构造查询引擎并发起查询
   query_engine = index.as_query_engine()
   response = query_engine.query("请问这份文档主要讲了些什么？")
   print(response)
   ```
   这样，llama_index 会使用你设置的 Gemini 模型生成响应。

以上方法已在多个实战案例中使用，例如在[LLM之RAG实战](citeturn0search0)和 GitHub 上相关示例项目中都有详细说明。注意，如果你需要使用 Gemini 的其他型号（例如 gemini-1.5-pro-latest），可以在 Gemini 初始化时传入相应参数，如：
```python
Settings.llm = Gemini(api_key=os.environ["GOOGLE_API_KEY"], model_name="models/gemini-1.5-pro-latest")
```

这样，你就可以在 llama_index 中调用 Google 的 Gemini 大模型进行文档索引、检索与生成任务了。


报错：
```
google.api_core.exceptions.RetryError: Timeout of 60.0s exceeded, last exception: 503 failed to connect to all addresses; last error: UNAVAILABLE: ipv4:142.250.77.10:443: Failed to connect to remote host: Timeout occurred: FD shutdown
WARNING: All log messages before absl::InitializeLog() is called are written to STDERR
E0000 00:00:1739367642.689011 19299647 init.cc:232] grpc_wait_for_shutdown_with_timeout() timed out.
```

补充信息：我的 mac 上开了代理，chrome 浏览器中是可以访问Google 的aistudio后台的

回复：

这个错误通常表示在使用 Gemini API 时，gRPC 客户端无法通过代理成功连接到 Google 的服务器，导致超时。虽然 Chrome 浏览器能正常访问 aistudio 后台，但 gRPC 请求默认不会自动使用你在系统或浏览器中配置的代理。你可以尝试以下几个方向解决问题：

1. **配置 gRPC 的代理设置**  
   gRPC 支持通过环境变量配置 HTTP 代理。你可以试试设置环境变量（例如在终端或代码开头设置）：
   - `http_proxy` 和 `https_proxy`：例如
     ```bash
     export http_proxy="http://127.0.0.1:你的代理端口"
     export https_proxy="http://127.0.0.1:你的代理端口"
     ```
     或者在 Python 中：
     ```python
     import os
     os.environ["http_proxy"] = "http://127.0.0.1:你的代理端口"
     os.environ["https_proxy"] = "http://127.0.0.1:你的代理端口"
     ```
   这样 gRPC 可能会遵循这些环境变量，建立连接。

2. **检查代理设置是否适用于 gRPC**  
   有时候 gRPC 使用的连接库可能不完全支持 HTTP 代理。如果你的代理需要认证或者使用特殊协议，可以尝试查阅 [gRPC 官方文档](https://grpc.io/docs/guides/) 或搜索 “grpc proxy configuration” 相关内容，确保代理配置正确。

3. **增加超时时间**  
   如果网络状况较差，也可以尝试延长超时时间，但通常根本原因在于连接问题而不是请求耗时。例如可以查阅 Google API 的客户端配置，看是否支持调整超时参数，不过这只是缓解，不能解决代理未生效的问题。

4. **使用 VPN 或其他网络工具**  
   如果配置代理依然无法生效，尝试临时关闭系统代理或者切换 VPN 连接，看是否能直接连接。如果能直接连接，说明问题确实出在代理设置上。也可以考虑在代码中使用支持 gRPC 代理的第三方工具。

总结：请确保你在运行代码的环境中正确设置了 `http_proxy` 和 `https_proxy` 环境变量，或者使用其他支持 gRPC 的代理配置方法。这样通常可以解决“Timeout of 60.0s exceeded… UNAVAILABLE”这类错误。

### 问题记录

#### 01 调用本地嵌入模型时报错

2025-02-12 

ImportError: llama-index-embeddings-huggingface package not found, please run pip install llama-index-embeddings-huggingface

解决方案：

pip install llama-index-embeddings-huggingface

#### 02 第三方平台调用不了 api

2025-02-12 

比如 302、硅基流动等。

总是报错调用的 api 跑到 OpenAI 的官网。

最后无意中发现 OpenAI 里传 url 的参数写错了，拷的之前的有个 base_url，这边的对象里参数应该是 api_base。

Settings.llm = OpenAI(
    api_base=base_url,
    api_key=api_key,
    model_name=model_name
)

#### 03 向量化的时候不能用异步

2025-02-14

DeepSeek 给的如下代码：

```py
        index = VectorStoreIndex(
            nodes,
            storage_context=storage_context,
            show_progress=True,
            use_async=True
        )
```

报错：

llama_index.vector_stores.weaviate._exceptions.AsyncClientNotProvidedError: Async method called without WeaviateAsyncClient provided. Pass the async weaviate client to be used via `weaviate_client` to the constructor of WeaviateVectorStore.

之前一直没弄明白，后来发现是不支持异步，看报错信息 `weaviate_client` 才支持异步，`weaviate_client` 应用是数据库在云端。

去掉即可。

```py
        index = VectorStoreIndex(
            nodes,
            storage_context=storage_context,
            show_progress=True	#显示进度
        )
```




通过下列方法将文档的摘要和文档内容向量化后存入 weaviate 向量数据库中。

```py
    summary_index = SummaryIndex(nodes)
    vector_index = VectorStoreIndex(nodes)
```

用如下方法可以将文档内容从向量数据库中取出索引，那么如何取出摘要的索引。

```py
    vector_store = WeaviateVectorStore(
        weaviate_client=client, 
        index_name=index_name
    )
```

#### 04 llamaindex通过大模型向量检索获得的答案跟使用大模型提问的获得的答案是两回事

llamaindex通过大模型向量检索获得的答案跟使用大模型提问的获得的答案是两回事，之前一直以为是通过个东西。

换句话说：llamaindex通过大模型向量检索，其目的是为了获得检索的上下文，而不是最后的答案。最后的答案是要用额外的大模型将问题上下文合并后单独提给大模型。

如何发现问题的：每次检索后提问获得的答案好简单。同样的向量数据库和问题，在 page assist 里提问就很详细，最后终于找到问题了。

之前的代码：

```py
def retrieval_from_documents_llamaindex(prompt, index_name, similarity_top_k):
    # 连接本地 Weaviate
    client = weaviate.connect_to_local()

    vector_store = WeaviateVectorStore(
        weaviate_client=client, 
        index_name=index_name
    )

    vector_index = VectorStoreIndex.from_vector_store(vector_store)
    query_engine = vector_index.as_query_engine(similarity_top_k=similarity_top_k)

    response = query_engine.query(prompt)
    print(str(response))
    # print(len(response.source_nodes))
    for n in response.source_nodes:
        print(n.metadata)
        print(n.text)
        print("----------------------------------------------------------")

    client.close()  # Free up resources
```


修改后的代码：

```py
def retrieval_from_documents(question, index_name, similarity_top_k):
    # 连接本地 Weaviate
    client = weaviate.connect_to_local()

    vector_store = WeaviateVectorStore(
        weaviate_client=client, 
        index_name=index_name
    )

    vector_index = VectorStoreIndex.from_vector_store(vector_store)
    query_engine = vector_index.as_query_engine(similarity_top_k=similarity_top_k)

    response = query_engine.query(question)
    context = "\n".join([n.text for n in response.source_nodes])

    prompt_template = ChatPromptTemplate.from_messages(
        [("system", system_template), ("user", "{context}")]
    )
    prompt = prompt_template.invoke({"context": context, "question": question})

    response = model.stream(prompt)
    for chunk in response:
        print(chunk.content, end='', flush=True)
    # print(response.content)

    client.close()  # Free up resources
```









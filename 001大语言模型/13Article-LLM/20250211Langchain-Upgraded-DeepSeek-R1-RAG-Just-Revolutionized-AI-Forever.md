## 20250211Langchain-Upgraded-DeepSeek-R1-RAG-Just-Revolutionized-AI-Forever

[Langchain (Upgraded) + DeepSeek-R1 + RAG Just Revolutionized AI Forever | by Gao Dalie (高達烈) | Jan, 2025 | Towards AI](https://pub.towardsai.net/langchain-upgraded-deepseek-r1-rag-just-revolutionized-ai-forever-27dcbb0e3493)

Gao Dalie (高達烈)

Towards AI

Jan 29, 2025

Last week, I made a video about DeepSeek-V3, and it caused a huge stir in the global AI community.

上周，我制作了一个关于 DeepSeek-V3 的视频，在全球 AI 社区引起了很大的反响。

Two Days ago, a Chinese DeepSeek released the inference-based large-scale language model “DeepSeek-R1” as open source!

两天前，中国的 DeepSeek 公司开源了基于推理的大规模语言模型（Large Language Model，LLM)「DeepSeek-R1」！

It’s said to perform just as well as OpenAI’s most accurate inference model, ‘o1.’ What’s even more impressive is that It is an incredibly price-breaking model with an API price of less than 1/25 of OpenAI o1. On top of that, it’s been open-sourced under the highly flexible MIT license, so anyone can download and use the model

据称，它的性能与 OpenAI 最精确的推理模型 'o1' 不相上下。更令人印象深刻的是，它是一款极具性价比的模型，API 价格仅为 OpenAI o1 的 1/25。更重要的是，它已采用极其灵活的 MIT 许可证开源，任何人都可以下载并使用该模型。

As soon as the R1 model came out this time, it not only refuted the previous statement of distilling OpenAI o1, but the official also directly said: “We can tie with the open source version of o1.”

这次 R1 模型一经发布，不仅驳斥了之前关于从 OpenAI 的 o1 模型中进行知识提炼的说法，而且官方还直接宣称：「我们的模型可以与 o1 模型的开源版本性能相当。」

It is worth mentioning that R1 breaks through the previous model training methods and does not use any SFT data at all. It only trains the model through pure RL. This shows that R1 has learned to think about problems by itself — which is actually more in line with human thinking. rule.

值得一提的是，R1 突破了以往的模型训练方法，完全没有使用任何有监督微调（Supervised Fine-Tuning，SFT）数据，而仅仅通过纯强化学习（Reinforcement Learning，RL）来训练模型。这表明 R1 已经学会独立思考，而这种方式实际上更加贴近人类的思维模式。

While I wanted to develop the RAG chatbot, I found that LangChain made huge updates before I developed the RAG chatbot with it. Unfortunately, it does not remember the conversation content like ChatGPT, and it also cannot input new data or be trained to answer specific questions like a customer service chatbot

虽然我计划开发 RAG 聊天机器人，但发现 LangChain 在我开始之前就经历了重大更新。遗憾的是，它不具备像 ChatGPT 那样的对话记忆功能，也无法像客服聊天机器人那样导入新数据或通过训练来回答特定问题。

So, Let me give you a quick demo of a live chatbot to show you what I mean.

接下来，我将快速演示一个实时聊天机器人，以便更直观地说明我的想法。

I will upload a PDF that includes images and then ask the chatbot a question: ‘Summarize this PDF.’ Feel free to ask any questions you want. If you look at how the chatbot generates the output, you will see that the PDF file stores its content in a temporary file, processes it with PDFPlumberLoader to extract complex data like tables, and cleans up the temporary file.

我会上传一个包含图像的 PDF 文档，并向聊天机器人提出一个问题：「总结这份 PDF 文档」。您可以随时提出任何问题。观察聊天机器人生成结果的过程，您会发现，PDF 文件首先将自身内容存储在一个临时文件中，然后利用 PDFPlumberLoader 对其进行处理，提取其中的表格等复杂结构化数据，最后清理该临时文件。

It uses SemanticChunker to split documents into semantic chunks and FAISS for efficient similarity-based search. The retriever finds the top 3 most similar chunks for a query and uses history_aware_retriever to enhance the agent’s ability to incorporate the entire conversation history into the retrieval process.

它使用 SemanticChunker 将文档分割成语义分块，并使用 FAISS 进行高效的基于相似性的搜索。检索器找到与查询最相似的前 3 个分块，并使用历史感知检索器（history_aware_retriever）来增强 AI 智能体将完整的对话历史整合到检索过程中的能力。

It also integrates context_chain for external input data and docs_chain for conversation records, using create_retrieval_chain to form a complete retrieval process. It handles context-aware responses by verifying if documents are uploaded, retrieving context, and generating responses with an RAG chain

它还整合了 `context_chain` 用于处理外部输入数据，以及 `docs_chain` 用于记录对话历史。通过 `create_retrieval_chain` 函数，将两者结合，构建完整的检索流程。该流程通过以下步骤处理具备上下文感知的回复：首先验证是否已上传相关文档，然后检索相关上下文信息，最后使用 RAG（Retrieval-Augmented Generation）链生成最终回复。

By the end of this video, you will understand how Deepseek R1 is trained and how to use Deepseek-R1 with RAG.

在本视频结束时，你将会明白 Deepseek R1 是如何训练的，以及如何将 Deepseek-R1 应用于 RAG。

### Overview of DeepSeek R1 learning method

DeepSeek R1 is characterized by its post-training using reinforcement learning (RL). In general, large-scale language models are developed through the following steps:

1 Pre-training: A large corpus creates a model that “predicts the next word.”

预训练：利用大型语料库训练出一个能够「预测下一个 Token」的模型。

2 Supervised fine-tuning (SFT): High-quality, human-created instruction-response pairs are used to fine-tune the model for a specific task.

监督式微调（SFT)：使用高质量的人工标注的指令 - 响应数据对模型进行微调，使其适应特定任务。

3 RLHF (Reinforcement Learning with Human Feedback): Humans evaluate the model’s output and use the score as a reward to update the model.

RLHF（Reinforcement Learning with Human Feedback，基于人类反馈的强化学习)：通过人类评估模型的输出，并将评估分数作为奖励信号来更新模型。

DeepSeek R1 reportedly performed reinforcement learning, especially step 3, on a large scale. Additionally, they explored an approach by applying RL directly, without the conventional SFT (a version called DeepSeek-R1-Zero), and then added SFT to complete DeepSeek R1. This method is said to have promoted the model’s internal thought process (chain-of-thought) and self-verification.

据报道，DeepSeek R1 在大规模上使用了强化学习，特别是第三步。此外，他们还探索了一种直接应用强化学习（RL）的方法，即不使用传统的 SFT（他们称之为 DeepSeek-R1-Zero 版本），而是直接应用强化学习，然后再加入 SFT 来完成 DeepSeek R1 的训练。据说，这种方法能够促进模型内部的思考过程（chain-of-thought，思维链）和自我验证能力。

Normally, handling the chain of thought effectively requires some SFT data and human labels. However, DeepSeek-R1-Zero claims to have achieved inference power through RL alone, without going through SFT. This approach offers the following advantages:

1 Reducing the cost of large-scale data collection

降低大规模数据采集的成本。

2 Enabling self-correction for unknown tasks and complex situations

针对未知的任务和复杂情境，启用自我修正功能。

However, models that have not gone through SFT completely still have issues such as text being somewhat difficult to read and unintended multilingual content.

然而，那些没有经过完整的 SFT（监督式微调）的模型，仍然存在一些问题，比如文本可读性较差，以及出现意料之外的多语言内容。

### Let’s Build The APP

Let us now explore step by step and unravel the answer to how to create RAG APP. we will install the libraries that support the model. For this, we will do a pip install requirements

让我们构建应用现在，让我们一步步探索，揭开如何创建 RAG 应用的奥秘。我们将安装支持模型的必要库。为此，我们将使用 pip 安装 requirements 文件中的依赖项。

pip install -r requirements.txt

The next step is the usual one where we will import the relevant libraries, the significance of which will become evident as we proceed.

接下来是常规操作，我们将导入必要的程序库，随着后续步骤的展开，您会逐渐体会到它们的重要性。

PDFPlumberLoader is a very powerful tool for processing complex structured data such as tables from PDF files. It can extract text, images, tables, fields, etc

PDFPlumberLoader 是一个非常强大的工具，可以处理 PDF 文件中复杂的结构化数据，例如表格。它能够提取文本、图像、表格和字段等信息。

SemanticChunker splits text into chunks based on semantic similarity, ensuring that related content stays together in the same chunk.

SemanticChunker 基于语义相似性将文本分割成块（chunks），确保语义相关的内容被保存在同一个块中。

and so on please, if you want to know more about the latest langchain upgrade where I will explain it in detail

接下来，我将详细介绍最新的 Langchain 升级，如果您想了解更多信息。

```python
import os
import streamlit as st
from langchain_community.document_loaders import PDFPlumberLoader
from langchain_experimental.text_splitter import SemanticChunker
from langchain_huggingface import HuggingFaceEmbeddings
import os
from langchain_community.vectorstores import FAISS
from langchain_core.prompts import ChatPromptTemplate，MessagesPlaceholder
from langchain.chains.history_aware_retriever import create_history_aware_retriever
from langchain.chains.combine_documents import create_stuff_documents_chain
from langchain.chains.retrieval import create_retrieval_chain
from langchain_core.messages import AIMessage，HumanMessage
import tempfile
from langchain_openai.chat_models.base import BaseChatOpenAI
```

I create a function to handle an uploaded file using a temporary file to store its content. I then process the PDF with PDFPlumberLoader to process complex structured data such as tables from PDF files, ensuring I clean up the temporary file afterwards to keep the system tidy. Finally, I return the extracted data for further use.

我创建了一个函数来处理上传的文件，该函数使用临时文件来存储文件内容。然后，我使用`PDFPlumberLoader` 来加载 PDF 文件，它可以处理复杂结构的 PDF 数据，例如表格。为了保持系统的整洁，我会确保在处理完毕后清理这些临时文件。最后，函数会返回提取的数据，以供后续流程使用。

```python
def process_uploaded_file(uploaded_file):

    with tempfile.NamedTemporaryFile(delete=False, suffix='.pdf') as tmp_file:
        tmp_file.write(uploaded_file.getvalue())
        loader = PDFPlumberLoader(tmp_file.name)
        documents = loader.load()
    os.unlink(tmp_file.name)
    return documents
```

I create a function to process a list of documents and build a retriever for similarity-based searches. First, I use the SemanticChunker with OpenAIEmbeddings to split the documents into smaller chunks while preserving semantic relationships, ensuring related content stays grouped together.

我创建了一个函数来处理文档列表，并构建一个基于相似性搜索的检索器。首先，我使用带有 OpenAI 嵌入（OpenAIEmbeddings）的 SemanticChunker（SemanticChunker）将文档分割成更小的块，同时保留语义关系，确保相关内容保持在一起。

After confirming the splitting process, I developed a vector store using FAISS, which organizes the chunks for efficient similarity search.

确认分割流程后，我使用 FAISS 构建了一个向量数据库，它能整理分块后的数据，从而实现高效的相似度搜索。

Finally, I return a retriever that can find the top 3 most similar chunks for a given query, making the document retrieval process both accurate and efficient.

最终，我返回一个检索器，它可以根据给定的查询，找到最相似的 3 个数据块，从而保证文档检索的准确性和效率。

```python
def get_vs_retriever_from_docs(doc_list):

    text_splitter = SemanticChunker(HuggingFaceEmbeddings())
    documents = text_splitter.split_documents(doc_list)
    st.write('Document splitting done')
    
    
    embedder = HuggingFaceEmbeddings()
    vector = FAISS.from_documents(documents, embedder)

    return vector.as_retriever(search_type="similarity", search_kwargs={"k": 3})
```

I create the init_ui() function to set up a user-friendly interface for uploading and analyzing PDF documents using Streamlit. First, I configure the page with a title and descriptive header.

我创建了 `init_ui（)` 函数，用于设置一个用户友好的界面，以便通过 Streamlit 上传和分析 PDF 文档。首先，我使用标题和描述性标题来配置页面。

I then initialize session state variables to manage the retriever, chat history, and upload status. Next, I provide a file uploader widget for users to upload PDF files.

我随后初始化会话状态变量，用于管理检索器（retriever）、聊天历史和上传状态。接下来，我提供了一个文件上传功能，用户可以通过它上传 PDF 文件。

Once a file is uploaded, I process it to extract its content, create a retriever using get_vs_retriever_from_docs, and store it in the session state for further use. Finally, I notify the user of the successful document processing with a success message.

一旦文件被上传，我会对其进行处理以提取内容，使用 `get_vs_retriever_from_docs` 创建一个检索器（retriever），并将其存储在会话状态中，以便后续使用。最后，我会发送一条成功消息，通知用户文档处理完毕。

```python
def init_ui():
    st.set_page_config(page_title='Document uploader')
    st.markdown('#### :books:🧙Gao Dalie (高達烈): Your Document Summarizer')
    st.markdown("<h8 style='text-align: right; color: green;'>*Share the pdf of the book you want to read*</h8>", unsafe_allow_html=True)
    
    if "vector_store" not in st.session_state:
        st.session_state.vector_store = None
    if "chat_history" not in st.session_state:
        st.session_state.chat_history = []  
    if "doc_upload" not in st.session_state:
        st.session_state.doc_upload = False

    uploaded_file = st.file_uploader("Upload PDF", type=["pdf"])
    if uploaded_file:
        docs = process_uploaded_file(uploaded_file)
        if docs:
            retriever = get_vs_retriever_from_docs(docs)
            st.session_state.vector_store = retriever
            st.session_state.doc_upload = True
            st.success("Document processed successfully")
```

I create the get_related_context() function to improve the retrieval of relevant information in a conversational system. First, I initialize the Ollama model (deepseek-r1) to process user inputs.

我创建了 `get_related_context（)` 函数，旨在提升对话系统中相关信息的检索效果。首先，我初始化 Ollama 模型（deepseek-r1），用于处理用户输入。

Then, I define a prompt template that combines the chat history and user input, instructing the model to generate a search query based on the ongoing conversation.

然后，我设计了一个提示模板，它将聊天记录和用户输入整合在一起，引导模型根据当前的对话内容生成搜索查询。

Finally, I use create_history_aware_retriever to enhance the agent's ability to incorporate the entire conversation history into the retrieval process.

```python
def get_related_context(vector_store):

    # llm = Ollama(model="deepseek-r1")
  
    
    llm = BaseChatOpenAI(
        model='deepseek-reasoner', 
        openai_api_key='sk-68f459660c7b4d179e074cbedce962c0', 
        openai_api_base='https://api.deepseek.com',
        max_tokens=1024
    )
    prompt = ChatPromptTemplate.from_messages([
        ("system", "Generate a search query based on the conversation."),
        ("user", "{input}")
    ])
    return create_history_aware_retriever(llm, vector_store, prompt)
```

In this function, I designed a function that integrates two core chains:

在这个函数中，我设计并整合了两个核心链：

1 context_chain Responsible for finding external input data

2 Responsible for finding conversation records

context_chain 负责寻找外部输入数据，并负责寻找对话记录。

Finally, use it retrieval_chain = create_retrieval_chain(context_chain, docs_chain) to create a chain that can retrieve conversations and external input data, and complete a chain that can allow natural conversations.

最终，利用 context_chain 和 docs_chain 创建检索链（retrieval_chain），即 `retrieval_chain = create_retrieval_chain（context_chain，docs_chain)`，该检索链可以检索对话和外部输入数据，从而构建一个能够进行自然对话的链。

The conversation record needs to create a List storage by itself, which is chat_history the part.

需要创建一个列表来存储对话记录，这部分内容对应于 `chat_history`。

```python
def get_context_aware_prompt(context_chain):
    # llm_! = Ollama(model="deepseek-r1")
    
    llm = BaseChatOpenAI(
        model='deepseek-reasoner', 
        openai_api_key='sk-68f459660c7b4d179e074cbedce962c0', 
        openai_api_base='https://api.deepseek.com',
        max_tokens=1024
    )
    prompt = ChatPromptTemplate.from_messages([
       ("system", "Answer questions using the provided context:\n\n{context}"),
       ("user", "{input}")
   ])
    # st.write(docs_chain)
    return create_retrieval_chain(context_chain, docs_chain)
```

In this function, I handle the process of generating a context-aware response for a given query. I start checking if the necessary documents are uploaded.

在这个函数中，我处理为给定的查询生成上下文感知的响应的过程。函数开始时，会检查是否已上传必要的文件。

If no documents are uploaded, I return an error. Once the documents are verified, I retrieve a context chain to access relevant information from the uploaded documents. If retrieving the context fails, I return an error.

如果没有上传任何文档，系统会报错。文档验证通过后，系统会提取一个上下文链（context chain），用于访问已上传文档中的相关信息。如果提取上下文信息失败，系统也会报错。

I then create an RAG chain that combines the context with the conversation history and the user’s query to generate a response. Finally, I invoke the RAG chain, process the response, and return the generated answer.

然后，我创建一个 RAG 链（RAG chain），该 RAG 链会将上下文、对话历史以及用户的查询整合起来，以生成响应。最后，我执行 RAG 链（RAG chain），分析处理响应，并返回生成的答案。

```python
def get_response(query: str) -> str:
    if not st.session_state.vector_store:
        return "Error: Please upload documents first"
    try:
        context_chain = get_related_context(st.session_state.vector_store)
        # st.write(context_chain)
        if not context_chain:
            return "Error: Failed to process context"

        rag_chain = get_context_aware_prompt(context_chain)
        # st.write(rag_chain)
        current_history = st.session_state.chat_history[-2:] if len(st.session_state.chat_history) > 1 else []
        return rag_chain.invoke({
            "chat_history": current_history,
            "input": query
        })["answer"].do
    except Exception as e:
        return f"Error: {str(e)}"
```

In this function, I set up and display a chat interface for user interaction. First, I loop through the stored chat history and display both user and AI messages in the chat.

在这个函数中，我搭建并呈现了一个用户交互的聊天界面。首先，程序会遍历已存储的聊天记录，并在界面上展示用户和 AI 的对话内容。

Then, I provide an input where the user can type a new question. If the user submits a query, I call the get_response function to generate an answer, and then I update the chat history with the new message and response.

接下来，我会提供一个输入框，用户可以在这里输入新的问题。如果用户提交了一个查询，我会调用 `get_response` 函数来生成答案，然后将新的消息和回复添加到聊天记录中，完成更新。

```python
def init_chat_interface():
    for message in st.session_state.chat_history:
        with st.chat_message("user" if isinstance(message, HumanMessage) else "assistant"):
            st.write(message.content)

    if prompt := st.chat_input("Ask a question...", disabled=not st.session_state.doc_upload):
        st.session_state.chat_history.append(HumanMessage(content=prompt))
        response = get_response(prompt)
        st.session_state.chat_history.append(AIMessage(content=response))

if __name__ == "__main__":
    init_ui()
    if st.session_state.vector_store:
        init_chat_interface()
```

### Conclusion

The launch of DeepSeek R1 is a technological breakthrough and a key milestone in AI’s democratization. Its open approach is reshaping our view of AI, allowing more people to contribute to its development.

DeepSeek R1 的发布是一项技术突破，也是人工智能（AI）普及的一个关键里程碑。其开放的方法正在重塑我们对人工智能的认知，让更多人能够参与到人工智能的开发中来。

Understanding concepts like the Retrieval Chain and the Conversation Retrieval Chain is crucial for using LangChain.

理解检索链（Retrieval Chain）和对话检索链（Conversation Retrieval Chain）等概念，对于使用 LangChain 至关重要。

As long as you understand the principles of these two Chains, you can not only know the operating principles behind customer service chatbots made with language models but also enable us to do similar applications.

只要理解这两种链的原理，不仅能了解基于语言模型构建的客服聊天机器人的运作方式，还能开发类似的应用。

However, LangChain is not just that. Many functions and tips need to be learned to create language model-related applications.

然而，LangChain 不仅于此。要创建基于语言模型的应用，还需要学习许多函数和技巧。

### Reference

https://github.com/deepseek-ai/DeepSeek-R1
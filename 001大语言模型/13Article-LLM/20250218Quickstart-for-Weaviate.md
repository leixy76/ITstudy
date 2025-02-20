Quickstart: locally hosted

[Locally hosted | Weaviate](https://weaviate.io/developers/weaviate/quickstart/local)

Prerequisites
Before we get started, install Docker and Ollama on your machine.

Then, download the nomic-embed-text and llama3.2 models by running the following command:

ollama pull nomic-embed-text
ollama pull llama3.2

We will be running Weaviate and language models locally. We recommend that you use a modern computer with at least 8GB or RAM, preferably 16GB or more.

Step 1: Set up Weaviate
1.1 Create a Weaviate database
Save the following code to a file named docker-compose.yml in your project directory.

```
version: '3.4'
services:
  weaviate:
    command:
    - --host
    - 0.0.0.0
    - --port
    - '8080'
    - --scheme
    - http
    image: cr.weaviate.io/semitechnologies/weaviate:1.28.4
    ports:
    - 8080:8080
    - 50051:50051
    volumes:
    - ./weaviate_data:/var/lib/weaviate
    restart: on-failure:0
    environment:
      QUERY_DEFAULTS_LIMIT: 25
      AUTHENTICATION_ANONYMOUS_ACCESS_ENABLED: 'true'
      PERSISTENCE_DATA_PATH: '/var/lib/weaviate'
      ENABLE_API_BASED_MODULES: 'true'
      ENABLE_MODULES: 'text2vec-ollama,generative-ollama'
      CLUSTER_HOSTNAME: 'node1'
```

1.2 Install a client library
We recommend using a client library to work with Weaviate. Follow the instructions below to install one of the official client libraries, available in Python, JavaScript/TypeScript, Go, and Java.

pip install -U weaviate-client

1.3: Connect to Weaviate
Now you can connect to your Weaviate instance.

The example below shows how to connect to Weaviate and perform a basic operation, like checking the cluster status.

import weaviate

client = weaviate.connect_to_local()

print(client.is_ready())  # Should print: `True`

client.close()  # Free up resources


Step 2: Populate the database
Now, we can populate our database by first defining a collection then adding data.

2.1 Define a collection
quickstart_create_collection.py

What is a collection?
A collection is a set of objects that share the same data structure, like a table in relational databases or a collection in NoSQL databases. A collection also includes additional configurations that define how the data objects are stored and indexed.

The following example creates a collection called Question with:

Ollama embedding model integration to create vectors during ingestion & queries, using the nomic-embed-text model, and
Ollama generative AI integrations for retrieval augmented generation (RAG), using the llama3.2 model.



2.2 Add objects
quickstart_import.py
We can now add data to our collection.

The following example:

Loads objects, and
Adds objects to the target collection (Question) using a batch process.

During a batch import, any failed objects can be obtained through batch.failed_objects. Additionally, a running count of failed objects is maintained and can be accessed through batch.number_errors within the context manager. This counter can be used to stop the import process in order to investigate the failed objects or references. Find out more about error handling on the Python client reference page.

Run this code to add the demo data.

Step 3: Queries
Weaviate provides a wide range of query tools to help you find the right data. We will try a few searches here.

3.1 Semantic search
quickstart_neartext_query.py
Semantic search finds results based on meaning. This is called nearText in Weaviate.

The following example searches for 2 objects whose meaning is most similar to that of biology.

Run this code to perform the query. Our query found entries for DNA and species.

Example full response in JSON format
If you inspect the full response, you will see that the word biology does not appear anywhere.

Even so, Weaviate was able to return biology-related entries. This is made possible by vector embeddings that capture meaning. Under the hood, semantic search is powered by vectors, or vector embeddings.

Here is a diagram showing the workflow in Weaviate.

Where did the vectors come from?
Weaviate used the locally hosted Ollama model to generate a vector embedding for each object during import. During the query, Weaviate similarly converted the query (biology) into a vector.

As we mentioned above, this is optional. See Starter Guide: Bring Your Own Vectors if you would prefer to provide your own vectors.

More search types available
Weaviate is capable of many types of searches. See, for example, our how-to guides on similarity searches, keyword searches, hybrid searches, and filtered searches.

3.2 Retrieval augmented generation
Retrieval augmented generation (RAG), also called generative search, combines the power of generative AI models such as large language models (LLMs) with the up-to-date truthfulness of a database.

RAG works by prompting a large language model (LLM) with a combination of a user query and data retrieved from a database.

This diagram shows the RAG workflow in Weaviate.

The following example combines the same search (for biology) with a prompt to generate a tweet.

quickstart_rag.py





import weaviate
from weaviate.classes.config import Configure
import requests, json

def quickstart_create_collection_by_loacalmodel():
    client = weaviate.connect_to_local()

    questions = client.collections.create(
        name="Question",
        vectorizer_config=Configure.Vectorizer.text2vec_ollama(     # Configure the Ollama embedding integration
            api_endpoint="http://host.docker.internal:11434",       # Allow Weaviate from within a Docker container to contact your Ollama instance
            model="bge-m3:latest",                               # The model to use
        ),
        generative_config=Configure.Generative.ollama(              # Configure the Ollama generative integration
            api_endpoint="http://host.docker.internal:11434",       # Allow Weaviate from within a Docker container to contact your Ollama instance
            model="deepseek-r1:14b",                                       # The model to use
        )
    )

    client.close()  #


def quickstart_create_collection():
    client = weaviate.connect_to_local()

    questions = client.collections.create(
        name="Question",
        vectorizer_config=Configure.Vectorizer.text2vec_ollama(     # Configure the Ollama embedding integration
            api_endpoint="http://host.docker.internal:11434",       # Allow Weaviate from within a Docker container to contact your Ollama instance
            model="bge-m3:latest",                               # The model to use
        ),
        generative_config=Configure.Generative.openai(
            model="deepseek-r1:14b",
        )
    )

    client.close()  #


def quickstart_import():
    client = weaviate.connect_to_local()

    resp = requests.get(
        "https://raw.githubusercontent.com/weaviate-tutorials/quickstart/main/data/jeopardy_tiny.json"
    )
    data = json.loads(resp.text)

    questions = client.collections.get("Question")

    with questions.batch.dynamic() as batch:
        for d in data:
            batch.add_object({
                "answer": d["Answer"],
                "question": d["Question"],
                "category": d["Category"],
            })
            if batch.number_errors > 10:
                print("Batch import stopped due to excessive errors.")
                break

    failed_objects = questions.batch.failed_objects
    if failed_objects:
        print(f"Number of failed imports: {len(failed_objects)}")
        print(f"First failed object: {failed_objects[0]}")

    client.close()  # Free up resources

def quickstart_neartext_query():
    client = weaviate.connect_to_local()

    questions = client.collections.get("Question")

    response = questions.query.near_text(
        query="biology",
        limit=2
    )

    for obj in response.objects:
        print(json.dumps(obj.properties, indent=2))

    client.close()  # Free up resources

def quickstart_rag():

    client = weaviate.connect_to_local()

    questions = client.collections.get("Question")

    response = questions.generate.near_text(
        query="biology",
        limit=2,
        grouped_task="Write a tweet with emojis about these facts."
    )

    print(response.generated)  # Inspect the generated text

    client.close()  # Free up resources


if __name__ == "__main__":
    quickstart_rag()
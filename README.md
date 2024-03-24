# Building a RAG application from scratch

This is a step-by-step guide to building a simple RAG (Retrieval-Augmented Generation) application using Pinecone and OpenAI's API. The application will allow you to ask questions about any YouTube video.

Training Video [HERE](https://www.youtube.com/watch?v=BrsocJb-fAo&t=2098s&ab_channel=Underfitted)

## Setup

1. In this tutorial, use `in-memory vector store`, which needs extra installation `pip install "langchain[docarray]"` and `Get it with "Microsoft C++ Build Tools": https://visualstudio.microsoft.com/visual-cpp-build-tools/` which I didn't follow, I skip this part and directly use pinecone instead.
1. Create a virtual environment and install the required packages:

```bash
$ python3 -m venv .venv
$ source .venv/bin/activate
$ pip install -r requirements.txt
```

For [whisper](https://github.com/openai/whisper) installation, use `pip install git+https://github.com/openai/whisper.git` instead of `pip install whisper`.

2. Create a free Pinecone account and get your API key from [here](https://www.pinecone.io/).
   If you don't have choice for regin setting, we are probably same using Iowa, US. <br>
   So here is setting `PINECONE_API_ENV="us-central1-gcp"`

3. Create a `.env` file with the following variables:

```bash
OPENAI_API_KEY = [ENTER YOUR OPENAI API KEY HERE]
PINECONE_API_KEY = [ENTER YOUR PINECONE API KEY HERE]
PINECONE_API_ENV = [ENTER YOUR PINECONE API ENVIRONMENT HERE]
```

4. Bug fix
   I did report issue in Author's github, [HERE](https://github.com/svpino/youtube-rag/issues/2).
   Instead of using PineconeVectorStore, got unAuth error, I use Pinecone directly.

```Py
from langchain_pinecone import Pinecone

import os
os.environ['PINECONE_API_KEY'] = "PINECONE_API_KEY"
index_name = "youtube-index"

pinecone = Pinecone.from_documents( index_name = index_name,
                                    documents = documents,
                                    embedding = embeddings)
```

## 💖 Conclusion, this is good tutorial for star learnning Langchain whisper, audio transcription, and RAG. I enjoy it.

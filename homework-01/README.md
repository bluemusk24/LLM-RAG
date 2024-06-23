## 1. Large Language Model Project 1

#### In this project, we'll learn more about search and use Elastic Search for practice.

* Notebook for this project is <https://github.com/bluemusk24/LLM-RAG/blob/main/homework-01/llm-homwork-01.ipynb>

* I ran this code below to download Elastic search image and start the container locally:
```bash
docker run -it \                 
   --name elasticsearch \
   -p 9200:9200 \
   -p 9300:9300 \
   -e "discovery.type=single-node" \
   -e "xpack.security.enabled=false" \
   docker.elastic.co/elasticsearch/elasticsearch:8.4.3
```

* Run this to confirm if Elastic search is up and running
```bash
curl http://localhost:9200
```

#### Get the Data for this project

* Run this code snippet
```bash
pip install requests

import requests 

docs_url = 'https://github.com/DataTalksClub/llm-zoomcamp/blob/main/01-intro/documents.json?raw=1'
docs_response = requests.get(docs_url)
documents_raw = docs_response.json()

documents = []

for course in documents_raw:
    course_name = course['course']

    for doc in course['documents']:
        doc['course'] = course_name
        documents.append(doc)
```

#### Calculate the number Token for the prompt using OpenAI 'gpt-4o' model

* Install the token library and run these codes below:
```bash
pip install tiktoken
```

* Run these codes:

```bash
import tiktoken

encoding = tiktoken.encoding_for_model("gpt-4o")

len(encoding.encode(text=prompt))
```


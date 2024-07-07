# Running Ollama with Docker

```bash
docker run -it \
    --rm \
    -v ollama:/root/.ollama \
    -p 11434:11434 \
    --name ollama \
    ollama/ollama
```

## To get the version of the running Ollama container

* run these codes to enter inside the Ollama container and get the version

```bash
docker exec -it ollama bash

ollama -v
```

## Downloading an LLM (gemma:2b) from Ollama

* run these codes to enter inside the Ollama container and pull the model:

```bash
docker exec -it ollama bash

ollama pull gemma:2b
```

* run these codes in a new terminal to get the metadata of the gemma:2b model

```bash 
cd /root/.ollama

cd models/manifests/registry.ollama.ai/library/gemma

cat 2b
```

## Running the LLM - gemma:2b with a prompt (10 * 10)

```bash
ollama run gemma:2b
```

## Downloading the weights and mapping ollama to local directory

* run these codes to create local directory [ollama_files](https://github.com/bluemusk24/LLM-RAG/tree/main/homework-02/ollama_files) and run the container

```bash
mkdir ollama_files

docker run -it \
    --rm \
    -v ./ollama_files:/root/.ollama \
    -p 11434:11434 \
    --name ollama \
    ollama/ollama
```

* run these codes to pull the model and get the size of the folder  [ollama_files](https://github.com/bluemusk24/LLM-RAG/tree/main/homework-02/ollama_files)

```bash
docker exec -it ollama ollama pull gemma:2b 

du -hs ollama_files/
```

## Contents of the dockerfile to add more weights 

```bash
FROM ollama/ollama

COPY ./ollama_files/ /root/.ollama/
```

* build the image from the dockerfile and run the container

```bash
docker build -t ollama-gemma2b .

docker run -it --rm -p 11434:11434 ollama-gemma2b

ollama start
```

* the jupyter notebook for the aforementioned dockerfile is [gemma.ipynb](https://github.com/bluemusk24/LLM-RAG/blob/main/homework-02/gemma.ipynb)
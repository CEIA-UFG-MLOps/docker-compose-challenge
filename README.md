# 🐳 Atividade Prática — MLOps com Docker Compose

Este projeto faz parte do grupo de estudos em **MLOps** e tem como objetivo aplicar conceitos fundamentais de **containerização** e **orquestração de serviços** utilizando **Docker** e **Docker Compose**.

## 🎯 Objetivo da atividade

Ao final desta atividade, você deverá ser capaz de:

* Criar e configurar **Dockerfiles** para aplicações backend e frontend.
* Montar um **ambiente multi-container** utilizando o **Docker Compose**.
* Fazer a comunicação entre um **servidor backend (API)** e uma **aplicação web frontend** dentro de containers diferentes.
* Entender o fluxo de comunicação em um ambiente que poderia futuramente ser integrado a pipelines de MLOps.

---

## 📁 Estrutura do projeto

```bash
mlops-docker-compose/
│
├── server/             # 🧠 Backend com endpoint que acessa modelo de linguagem via RAG
│   ├── app.py          
│   ├── requirements.txt
│   └── ...             
│
├── web/                # 💻 Frontend que consome o backend
│   ├── app.py          
│   ├── requirements.txt
│   └── ... 
|
| 
├── model/                # 🧠 Script para rodar modelo
│   ├── qwen.sh          
│   └── ...             
│
├── docker-compose.yml  # 🧩 Arquivo de orquestração (a ser criado pelo aluno)
│
└── README.md           # 📘 Este arquivo
```

---

## 🧪 Descrição dos componentes

### 🧠 Backend (`server/`)

O servidor fornece um **endpoint REST** (por exemplo, `/api/query`) que se comunica com um **modelo de linguagem com RAG (Retrieval-Augmented Generation)**.
Parte do código pode estar **incompleto**, e será necessário implementar ou ajustar o trecho faltante indicado por comentários como:

```python
# TODO: implementar chamada ao modelo RAG
```

---

### 💻 Frontend (`web/`)

A aplicação web possui uma interface simples que envia requisições ao backend e exibe as respostas.
O código também pode conter trechos faltantes com instruções como:

```javascript
// TODO: completar a função que faz a chamada à API
```

---

## 🧩 Tarefas do desafio

1. **Crie um Dockerfile para o backend (`server/`)**

   * Base: `python:3.10`
   * Instale dependências do `requirements.txt`
   * Exponha a porta usada (por exemplo, `8000`)
   * Execute a aplicação (ex: `uvicorn app:app --host 0.0.0.0 --port 8000`)

2. **Crie um Dockerfile para o frontend (`web/`)**

   * Base: `node:18`
   * Instale dependências via `npm install`
   * Exponha a porta usada (por exemplo, `3000`)
   * Execute o servidor (ex: `npm start`)

3. **Monte o `docker-compose.yml`**

   * Deve conter **dois serviços**: `server` e `web`
   * Ambos devem estar na mesma **bridge network**
   * O serviço `web` deve depender de `server` (usando `depends_on`)
   * Mapeie as portas locais (ex: `8000:8000` e `3000:3000`)

Exemplo de estrutura esperada (não completa!):

```yaml
version: "3.9"
services:
  server:
    build: ./server
    ports:
      - "8000:8000"
  web:
    build: ./web
    ports:
      - "3000:3000"
    depends_on:
      - server
```

---

## ▶️ Como executar

Após criar os arquivos necessários:

```bash
# Construir e iniciar os containers
docker compose up --build
```

Acesse:

* Frontend: [http://localhost:3000](http://localhost:3000)
* Backend API: [http://localhost:8000](http://localhost:8000)

---

## 🧩 Desafio bônus (opcional)

* Adicione um **volume** para o backend que armazene logs.
* Configure variáveis de ambiente no `docker-compose.yml` para controlar o host e porta do backend.
* Utilize uma **rede customizada** para isolar os containers.
* Adicione um serviço extra (ex: `redis` ou `postgres`) e conecte ao backend.

---

## 📘 Recursos de apoio

* [Documentação oficial do Docker](https://docs.docker.com/)
* [Documentação do Docker Compose](https://docs.docker.com/compose/)
* [Guia sobre Dockerfiles](https://docs.docker.com/engine/reference/builder/)

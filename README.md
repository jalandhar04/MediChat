# MediChat

An end-to-end medical chatbot powered by Generative AI. Ask health-related questions and get informed, accurate answers in real-time.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
  - [Clone Repository](#clone-repository)
  - [Create & Activate Conda Environment](#create--activate-conda-environment)
  - [Install Dependencies](#install-dependencies)
  - [Configure Environment Variables](#configure-environment-variables)
- [Usage](#usage)
  - [Indexing Documents](#indexing-documents)
  - [Running the App](#running-the-app)
- [AWS CI/CD Deployment](#aws-cicd-deployment)
  - [1. AWS Setup](#1-aws-setup)
  - [2. ECR & Docker](#2-ecr--docker)
  - [3. EC2 Self-Hosted Runner](#3-ec2-self-hosted-runner)
  - [4. GitHub Secrets](#4-github-secrets)
- [Contributing](#contributing)
- [License](#license)

---

## Features

- Conversational medical assistant using **Gemini 2.0 Flash**
- Semantic search via **HuggingFace** embeddings and **Pinecone** vector database
- Built with **Python**, **Flask**, and **LangChain**
- Modern, responsive chat UI with typing animations
- Easy local setup & AWS CI/CD deployment with GitHub Actions

## Tech Stack

- **Language & Framework**: Python 3.12, Flask
- **AI & LLM**: LangChain, Google Gemini 2.0 Flash
- **Embeddings**: HuggingFace Transformers (`all-MiniLM-L6-v2`)
- **Vector DB**: Pinecone
- **Frontend**: HTML5, Bootstrap 5, jQuery, CSS Glassmorphism
- **CI/CD & Hosting**: Docker, AWS ECR, EC2, GitHub Actions

## Prerequisites

- [Conda](https://docs.conda.io/en/latest/) installed
- AWS account (for deployment)
- GitHub account

## Installation

### Clone Repository

```bash
git clone https://github.com/jalandhar04/MediChat.git
cd MediChat
```

### Create & Activate Conda Environment

```bash
conda create -n medichat python=3.12 -y
conda activate medichat
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Configure Environment Variables

Create a `.env` file in the project root and add:

```ini
PINECONE_API_KEY="YOUR_PINECONE_API_KEY"
GEMINI_API_KEY="YOUR_GOOGLE_API_KEY"
```

> **Note**: Keep your keys secret. Do not commit `.env` to version control.

## Usage

### Indexing Documents

Generate and upload embeddings for your documents:

```bash
python store_index.py
```

### Running the App

```bash
python app.py
```

Open your browser at `http://localhost:8080` to start chatting.

## AWS CI/CD Deployment

Automate build & deployment via GitHub Actions.

### 1. AWS Setup

1. **IAM User**: Create with policies:
   - `AmazonEC2FullAccess`
   - `AmazonEC2ContainerRegistryFullAccess`
2. **ECR Repository**:
   ```text
   970547337635.dkr.ecr.ap-south-1.amazonaws.com/medicalchatbot
   ```

### 2. ECR & Docker

1. Build Docker image:
   ```bash
   ```

docker build -t medicalchatbot .

````
2. Tag & push to ECR:
   ```bash
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 970547337635.dkr.ecr.ap-south-1.amazonaws.com
docker tag medicalchatbot:latest 970547337635.dkr.ecr.ap-south-1.amazonaws.com/medicalchatbot:latest
docker push 970547337635.dkr.ecr.ap-south-1.amazonaws.com/medicalchatbot:latest
````

### 3. EC2 Self-Hosted Runner

1. Launch Ubuntu EC2 instance
2. Install Docker:
   ```bash
   ```

sudo apt-get update -y curl -fsSL [https://get.docker.com](https://get.docker.com) -o get-docker.sh sudo sh get-docker.sh sudo usermod -aG docker \$USER newgrp docker

```
3. Configure as GitHub Actions runner (Settings → Actions → Runners)

### 4. GitHub Secrets

In your repo settings, add:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_DEFAULT_REGION` (e.g. `ap-south-1`)
- `ECR_REPO` (e.g. `970547337635.dkr.ecr.ap-south-1.amazonaws.com/medicalchatbot`)
- `PINECONE_API_KEY`
- `GEMINI_API_KEY`


## Contributing

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -m 'Add feature'`)
4. Push and open a Pull Request

## License

MIT © [https://jalandharpaswan.com](https://jalandharpaswan.com)

```

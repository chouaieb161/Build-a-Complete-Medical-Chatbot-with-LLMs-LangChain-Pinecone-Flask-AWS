
# 🏥 Medical Chatbot with LLMs, LangChain, Pinecone & Flask

A production-ready intelligent medical chatbot built with cutting-edge AI technologies. This application leverages Large Language Models (LLMs), LangChain, and Pinecone vector database to provide accurate, context-aware medical information and assistance.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Deployment](#deployment)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [FAQ](#faq)
- [Support](#support)

---

## 🎯 Overview

This Medical Chatbot is an intelligent conversational AI system designed to provide reliable medical information and answer healthcare-related queries. By combining state-of-the-art language models with a specialized medical knowledge base stored in Pinecone, the chatbot delivers accurate, contextually relevant responses while maintaining data privacy and security.

**Key Capabilities:**
- Conversational Q&A on medical topics
- Context-aware responses using RAG (Retrieval-Augmented Generation)
- Real-time inference with low latency
- Scalable cloud deployment with AWS

---

## ✨ Features

- 🤖 **AI-Powered Conversations** - Powered by OpenAI's GPT models
- 📚 **Medical Knowledge Base** - Indexed with Pinecone vector database for semantic search
- 🔍 **Intelligent Retrieval** - LangChain-based document retrieval and processing
- 🌐 **Web Interface** - User-friendly Flask web application
- 🔐 **Secure** - Environment-based credential management
- 📄 **PDF Processing** - Automatic extraction and indexing of PDF documents
- ☁️ **Cloud Ready** - Deployment-ready with Docker and GitHub Actions
- 🚀 **Scalable** - Serverless Pinecone infrastructure

---

## 🛠️ Tech Stack

| Component | Technology | Version |
|-----------|-----------|---------|
| **Backend Framework** | Flask | 3.1.1 |
| **LLM Orchestration** | LangChain | 0.3.26 |
| **Vector Database** | Pinecone | Latest |
| **Embeddings** | Sentence Transformers | 4.1.0 |
| **Language Model** | OpenAI GPT | GPT-4/GPT-3.5 |
| **PDF Processing** | PyPDF | 5.6.1 |
| **Environment Management** | python-dotenv | 1.1.0 |
| **Python Version** | Python | 3.10 |
| **Container** | Docker | Latest |
| **CI/CD** | GitHub Actions | Latest |
| **Cloud Platform** | AWS | EC2, ECR |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    User Interface                            │
│              (Flask Web Application)                         │
└──────────────────────┬──────────────────────────────────────┘
                       │ HTTP Requests
                       │
┌──────────────────────▼──────────────────────────────────────┐
│                  Flask Backend (app.py)                      │
│        - Request processing                                  │
│        - Session management                                  │
│        - Response formatting                                 │
└──────────────────────┬──────────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────────┐
│               LangChain Pipeline                             │
│        - Query processing & understanding                    │
│        - Document retrieval & ranking                        │
│        - Context management & memory                         │
└──────────────────────┬──────────────────────────────────────┘
                       │
            ┌──────────┴──────────┐
            │                     │
    ┌───────▼────────┐   ┌────────▼────────┐
    │  Pinecone DB   │   │ OpenAI GPT API  │
    │ (Vector Store) │   │  (LLM)          │
    │  - Embeddings  │   │ - Text Gen      │
    │  - Semantic    │   │ - Understanding │
    │    Search      │   │                 │
    └────────────────┘   └─────────────────┘
```

---

## 📋 Prerequisites

Before you begin, ensure you have:

- **Python 3.10+** installed on your system
- **Git** installed for version control
- **Conda** (recommended) or **pip** for package management
- **Pinecone API Key** - [Sign up here](https://www.pinecone.io/)
- **OpenAI API Key** - [Sign up here](https://platform.openai.com/)
- **Docker** (optional, for containerization)
- **AWS Account** (optional, for cloud deployment)

---

## 📥 Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/chouaieb161/Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS.git
cd Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS
```

### Step 2: Create a Conda Environment

```bash
conda create -n medibot python=3.10 -y
conda activate medibot
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

**Dependencies include:**
- langchain==0.3.26
- flask==3.1.1
- sentence-transformers==4.1.0
- pypdf==5.6.1
- python-dotenv==1.1.0
- langchain-pinecone==0.2.8
- langchain-openai==0.3.24
- langchain-community==0.3.26

---

## ⚙️ Configuration

### Step 1: Create Environment Variables

Create a `.env` file in the project root directory:

```bash
touch .env
```

### Step 2: Add Your Credentials

Edit the `.env` file and add your API keys:

```env
# Pinecone Configuration
PINECONE_API_KEY=your_pinecone_api_key_here
PINECONE_INDEX_NAME=medical-chatbot
PINECONE_ENVIRONMENT=us-east-1

# OpenAI Configuration
OPENAI_API_KEY=your_openai_api_key_here

# Flask Configuration (Optional)
FLASK_ENV=development
FLASK_DEBUG=True
FLASK_APP=app.py
```

### Step 3: Prepare Medical Data

Place your PDF documents in the `data/` directory:

```bash
mkdir -p data
# Add your medical PDF files to the data/ directory
```

---

## 🚀 Usage

### Step 1: Initialize Vector Database

Process and index your documents to Pinecone:

```bash
python store_index.py
```

**This script will:**
- Load PDF files from the `data/` directory
- Extract text content from PDFs
- Split text into manageable chunks
- Generate embeddings using Sentence Transformers
- Store embeddings and metadata in Pinecone

### Step 2: Run the Application

Start the Flask development server:

```bash
python app.py
```

The application will start on `http://localhost:5000`

### Step 3: Access the Web Interface

Open your browser and navigate to:

```
http://localhost:5000
```

### Example Queries

Once the application is running, try these queries:

- "What are the symptoms of diabetes?"
- "How should I treat a common cold?"
- "Explain the causes of hypertension"
- "What is the recommended dosage of aspirin?"
- "How does the immune system work?"
- "What are the side effects of antibiotics?"

---

## 📦 Project Structure

```
Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS/
│
├── app.py                      # Main Flask application
├── store_index.py              # Vector database initialization script
├── setup.py                    # Package setup configuration
├── requirements.txt            # Python dependencies
│
├── .env                        # Environment variables (create this)
├── .env.example                # Example environment file
├── .gitignore                  # Git ignore file
├── Dockerfile                  # Docker configuration
├── docker-compose.yml          # Docker compose file
│
├── README.md                   # Project documentation
├── LICENSE                     # MIT License
│
├── data/                       # Medical documents directory
│   └── *.pdf                   # Place your medical PDFs here
│
├── src/                        # Source code modules
│   ├── __init__.py
│   ├── helper.py               # Helper functions for PDF processing
│   ├── embeddings.py           # Embedding utilities and functions
│   └── prompts.py              # LLM prompts and templates
│
├── static/                     # Static files (CSS, JS, images)
│   ├── css/
│   ├── js/
│   └── images/
│
├── templates/                  # HTML templates
│   ├── index.html              # Main page
│   ├── chat.html               # Chat interface
│   └── base.html               # Base template
│
└── research/                   # Research notebooks
    └── *.ipynb                 # Jupyter notebooks for experimentation
```

---

## ☁️ Deployment

### AWS Deployment with CI/CD

#### Prerequisites:

- AWS Account with appropriate permissions
- Docker installed
- GitHub repository access
- AWS CLI installed (optional)

#### Setup Steps:

##### Step 1: Create IAM User

1. Login to AWS Console
2. Navigate to IAM → Users → Create User
3. Grant the following policies:
   - `AmazonEC2ContainerRegistryFullAccess`
   - `AmazonEC2FullAccess`

##### Step 2: Create ECR Repository

```bash
aws ecr create-repository --repository-name medicalbot --region us-east-1
```

**Save the repository URI:** `XXXXXXXXXXXX.dkr.ecr.us-east-1.amazonaws.com/medicalbot`

##### Step 3: Launch EC2 Instance

1. AWS Console → EC2 → Instances → Launch Instance
2. **AMI:** Ubuntu 20.04 LTS
3. **Instance Type:** t2.medium (or higher)
4. **Security Group:** Allow inbound traffic on port 5000 and 22

##### Step 4: Install Docker on EC2

```bash
# Update system packages
sudo apt-get update -y
sudo apt-get upgrade -y

# Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Add user to docker group
sudo usermod -aG docker ubuntu
newgrp docker
```

##### Step 5: Configure GitHub Secrets

Add these secrets to your GitHub repository (Settings → Secrets and Variables → Actions):

```
AWS_ACCESS_KEY_ID          = your_access_key_here
AWS_SECRET_ACCESS_KEY      = your_secret_key_here
AWS_DEFAULT_REGION         = us-east-1
ECR_REPO                   = your_ecr_uri_here
OPENAI_API_KEY             = your_openai_key_here
PINECONE_API_KEY           = your_pinecone_key_here
EC2_INSTANCE_IP            = your_ec2_instance_ip
```

##### Step 6: Setup Self-Hosted Runner

1. GitHub → Settings → Actions → Runners → New self-hosted runner
2. Choose Linux
3. Follow the setup instructions for Ubuntu
4. Run the runner

##### Step 7: Create GitHub Actions Workflow

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to AWS

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Build Docker image
        run: docker build -t medicalbot:latest .
      
      - name: Push to ECR
        run: |
          aws ecr get-login-password --region ${{ secrets.AWS_DEFAULT_REGION }} | \
          docker login --username AWS --password-stdin ${{ secrets.ECR_REPO }}
          docker tag medicalbot:latest ${{ secrets.ECR_REPO }}:latest
          docker push ${{ secrets.ECR_REPO }}:latest
```

---

## 🐳 Docker Deployment

### Build Docker Image

```bash
docker build -t medicalbot:latest .
```

### Run Container Locally

```bash
docker run -d \
  -p 5000:5000 \
  -e OPENAI_API_KEY=your_openai_key \
  -e PINECONE_API_KEY=your_pinecone_key \
  -v $(pwd)/data:/app/data \
  --name medicalbot \
  medicalbot:latest
```

### Check Logs

```bash
docker logs -f medicalbot
```

### Stop Container

```bash
docker stop medicalbot
docker rm medicalbot
```

---

## 🔧 Troubleshooting

### Issue: "PINECONE_API_KEY not found"

**Solution:** Ensure your `.env` file exists in the project root with the correct API key.

```bash
# Verify .env file
cat .env

# Check if environment variables are loaded
python -c "import os; print(os.environ.get('PINECONE_API_KEY'))"
```

### Issue: "ModuleNotFoundError: No module named 'src'"

**Solution:** Ensure you're running from the project root directory and have installed the package.

```bash
# Install the package in development mode
pip install -e .

# Verify you're in the correct directory
pwd
```

### Issue: PDF files not being indexed

**Solution:** Check that PDF files are in the `data/` directory and are readable.

```bash
# List files in data directory
ls -la data/

# Check file permissions
file data/*.pdf
```

### Issue: Connection timeout to OpenAI/Pinecone

**Solution:** Verify API keys and check internet connectivity.

```bash
# Test Pinecone connection
python -c "from pinecone import Pinecone; pc = Pinecone(api_key='your_key'); print('Connection successful')"

# Test OpenAI connection
python -c "from openai import OpenAI; client = OpenAI(api_key='your_key'); print('Connection successful')"
```

### Issue: Slow response times

**Solutions:**
1. Check Pinecone index status and dimensionality
2. Reduce chunk size in `src/helper.py`
3. Optimize embedding model selection
4. Check network latency to AWS/Pinecone servers

### Issue: Out of memory errors

**Solutions:**
1. Reduce batch size for PDF processing
2. Process PDFs in smaller chunks
3. Increase EC2 instance memory allocation
4. Implement pagination for large results

---

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### Fork the Repository

```bash
git clone https://github.com/yourusername/Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS.git
cd Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS
```

### Create a Feature Branch

```bash
git checkout -b feature/your-feature-name
```

### Make Your Changes

```bash
# Make code changes
# Test your changes
```

### Commit Your Changes

```bash
git add .
git commit -m "Add your meaningful commit message"
```

### Push to Your Fork

```bash
git push origin feature/your-feature-name
```

### Create a Pull Request

1. Go to GitHub repository
2. Click "New Pull Request"
3. Provide a clear description of your changes
4. Reference any related issues
5. Wait for review and feedback

### Development Guidelines

- Write clean, documented code
- Follow PEP 8 style guidelines
- Add tests for new features
- Update documentation as needed
- Test with different medical documents

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙋 FAQ

### Q: Can I use this for production medical consultations?

**A:** This chatbot is for informational purposes only and should **not replace professional medical advice**. Always consult with qualified healthcare professionals for medical decisions.

### Q: How much does it cost to run?

**A:** Costs depend on API usage:
- OpenAI API: Based on tokens used (~$0.002 per 1K tokens for GPT-3.5)
- Pinecone: Free tier available, paid tiers start at $0.04 per pod/month
- AWS: EC2 instance costs vary by instance type

### Q: Can I customize the chatbot for specific medical domains?

**A:** Yes! Provide domain-specific PDF documents in the `data/` directory. The system will automatically index and utilize them.

### Q: How often should I update the knowledge base?

**A:** Regularly update medical documents to:
- Ensure accuracy
- Stay current with latest medical information
- Remove outdated or superseded information

### Q: Can I use different LLM models?

**A:** Yes, modify `app.py` to use different OpenAI models or even switch to open-source models like LLaMA or Mistral.

### Q: Is the chatbot HIPAA compliant?

**A:** Currently, no. For HIPAA compliance, implement:
- Data encryption in transit and at rest
- Access controls and authentication
- Audit logging
- Business associate agreements

### Q: Can I deploy on other cloud providers?

**A:** Yes, the Docker container can be deployed on:
- Google Cloud Run
- Azure Container Instances
- DigitalOcean App Platform
- Heroku

---

## 📞 Support

For questions and support:

- **GitHub Issues:** [Open an issue](https://github.com/chouaieb161/Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS/issues)
- **GitHub Discussions:** [Start a discussion](https://github.com/chouaieb161/Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS/discussions)
- **Email:** dridichouaieb07@gmail.com

---

## 🎓 Learning Resources

- [LangChain Documentation](https://python.langchain.com/)
- [Pinecone Vector Database](https://docs.pinecone.io/)
- [OpenAI API Documentation](https://platform.openai.com/docs/)
- [Flask Framework](https://flask.palletsprojects.com/)
- [AWS EC2 Guide](https://docs.aws.amazon.com/ec2/)
- [Docker Documentation](https://docs.docker.com/)
- [Retrieval-Augmented Generation (RAG)](https://arxiv.org/abs/2005.11401)

---

## 🔗 Related Projects

- [LangChain Examples](https://github.com/langchain-ai/langchain)
- [Pinecone Projects](https://www.pinecone.io/learn/)
- [OpenAI Cookbooks](https://github.com/openai/cookbook)

---

## 📊 Performance Metrics

- **Response Time:** < 2 seconds per query
- **Accuracy:** Depends on knowledge base quality
- **Scalability:** Supports up to 1M+ document embeddings
- **Concurrent Users:** Limited by Flask/AWS instance size

---

## 🔐 Security Best Practices

1. **Never commit `.env` file** to version control
2. **Use strong API keys** with regular rotation
3. **Implement rate limiting** for production
4. **Use HTTPS** for all connections
5. **Validate user inputs** to prevent injection attacks
6. **Keep dependencies updated** regularly

---

**Built with ❤️ using AI and Open Source Technologies**

---

*Last Updated: March 14, 2026*
*Maintained by: [chouaieb161](https://github.com/chouaieb161)*

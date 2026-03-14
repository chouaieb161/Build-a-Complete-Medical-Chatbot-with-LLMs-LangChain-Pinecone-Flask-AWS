# Medical Chatbot Documentation

## Project Overview
This project presents a complete medical chatbot built using modern technologies including LLMs, LangChain, Pinecone, Flask, and AWS. The chatbot assists users in retrieving medical information efficiently.

## Features
- Natural language processing capabilities
- Integration with various medical databases
- User-friendly interface

## Architecture
The architecture includes multiple components such as:
- **Frontend:** Built using Flask for handling user interactions.
- **LLMs:** Leveraging large language models for understanding and generating responses.
- **Pinecone:** Used for handling semantic search and vector databases.
- **AWS:** Deployed on Amazon Web Services for scalability.

## Installation Steps
1. Clone the repository:
   `git clone https://github.com/chouaieb161/Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS.git`
2. Navigate to the project directory:
   `cd Build-a-Complete-Medical-Chatbot-with-LLMs-LangChain-Pinecone-Flask-AWS`
3. Install the required dependencies:
   `pip install -r requirements.txt`

## Configuration
Set up environment variables as required:
- `FLASK_ENV=development`
- `AWS_ACCESS_KEY_ID=your_access_key`
- `AWS_SECRET_ACCESS_KEY=your_secret_key`

## Usage Examples
To start the Flask server, run:
`flask run`

Then navigate to `http://127.0.0.1:5000` in your web browser.

## Deployment Guide
Follow the instructions for deploying on AWS to ensure that the chatbot scales appropriately with usage.

## Troubleshooting
- Ensure all dependencies are properly installed.
- Check API keys and configurations.

## Contributing Guidelines
1. Fork the repository.
2. Create a new branch for your feature.
3. Submit a pull request.

## License
This project is licensed under the MIT License.
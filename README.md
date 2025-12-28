# AI-Spec-Driven Technical Book with Integrated RAG Chatbot

This project implements an AI-Spec-Driven Technical Book with Integrated RAG Chatbot following the Spec-Driven Development methodology. The system provides a Docusaurus-based static website hosting technical content with a RAG (Retrieval Augmented Generation) chatbot that grounds responses in the book's indexed content.

## Table of Contents
- [Features](#features)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Development](#development)
- [Deployment](#deployment)
- [Project Structure](#project-structure)
- [API Documentation](#api-documentation)

## Features
- Docusaurus-based static website for technical documentation
- RAG (Retrieval Augmented Generation) chatbot
- Content grounded in indexed book material
- Support for user-provided text analysis
- GitHub Pages deployment

## Architecture
The system is built with a modular architecture:
- **Frontend**: Docusaurus static site generator (hosted on GitHub Pages)
- **Backend**: FastAPI application with OpenAI integration
- **Database**: Neon Serverless Postgres for metadata and conversation state
- **Vector Storage**: Qdrant Cloud for semantic search and retrieval

## Prerequisites
- Node.js LTS (v18 or higher)
- Python 3.11+
- Git
- Access to OpenAI API
- Access to Qdrant Cloud (Free Tier)
- Neon Postgres account

## Setup

### 1. Clone the Repository
```bash
git clone <repository-url>
cd AI-Book
```

### 2. Frontend Setup (Documentation Site)
```bash
cd website
npm install
npm start
```
The documentation site will be available at `http://localhost:3000`.

### 3. Backend Setup
```bash
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 4. Environment Variables
Create a `.env` file in the backend directory:
```env
OPENAI_API_KEY=your_openai_api_key
QDRANT_URL=your_qdrant_cluster_url
QDRANT_API_KEY=your_qdrant_api_key
NEON_DATABASE_URL=your_neon_postgres_connection_string
SECRET_KEY=your_secret_key_for_fastapi
DEBUG=false
```

### 5. Start the Backend
```bash
cd backend/src
uvicorn main:app --reload --port 8000
```

## Development

### Frontend Development
The documentation site uses Docusaurus. To run in development mode:
```bash
cd website
npm start
```

### Backend Development
The backend uses FastAPI. To run in development mode:
```bash
cd backend/src
uvicorn main:app --reload
```

### Content Creation
Documentation content is stored in the `website/docs/` directory in Markdown format. To add new content:
1. Create a new `.md` file in the appropriate directory
2. Add it to the sidebar configuration in `website/sidebars.js`
3. Update the navigation as needed

## Deployment

### GitHub Pages
The frontend documentation site is deployed to GitHub Pages using GitHub Actions. The workflow is configured in `.github/workflows/deploy.yml`.

### Backend Deployment
The backend can be deployed to any cloud provider that supports Python applications. The current setup is designed to work with platforms like:
- AWS Elastic Beanstalk
- Google Cloud Run
- Azure App Service
- Railway
- Render

## Project Structure
```
AI-Book/
├── website/                 # Docusaurus documentation site
│   ├── docs/               # Documentation content
│   ├── src/                # Custom components
│   ├── static/             # Static assets
│   ├── docusaurus.config.js # Docusaurus configuration
│   ├── sidebars.js         # Navigation configuration
│   └── package.json        # Frontend dependencies
├── backend/                # FastAPI backend application
│   ├── src/
│   │   ├── models/         # Data models
│   │   ├── services/       # Business logic
│   │   ├── api/            # API endpoints
│   │   └── utils/          # Utility functions
│   ├── tests/              # Test files
│   └── requirements.txt    # Python dependencies
├── specs/                  # Specification files
├── history/                # Prompt history records
├── .github/                # GitHub configuration
│   └── workflows/          # GitHub Actions workflows
├── .gitignore             # Git ignore patterns
└── README.md              # This file
```

## API Documentation
The backend API follows REST principles and includes:
- `/chat` - Endpoint for chatbot interactions
- `/chat/history` - Endpoint for conversation history
- OpenAPI documentation available at `/docs` when running the backend

For detailed API documentation, see `specs/001-ai-book-rag-chatbot/contracts/chatbot-api.yaml`.

## Contributing
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License
This project is licensed under the MIT License - see the LICENSE file for details.
# My CrewAI Project

This is a CrewAI application built to demonstrate the power of autonomous AI agents working together.

## Setup

1. Clone this repository
2. Create a virtual environment:
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. Install dependencies:
   ```
   pip install -e .
   pip install -r requirements.txt
   ```
4. Copy `.env.example` to `.env` and fill in your API keys:
   - `OPENAI_API_KEY`: Your OpenAI API key
   - `PINECONE_API_KEY`: Your Pinecone API key
   - `PINECONE_INDEX`: Name of your Pinecone index

## Usage

Run the Flask web application:

```
python -m my_project.app
```

## API Endpoints

### Home
- **URL**: `/`
- **Method**: `GET`
- **Response**: JSON with API status and available endpoints documentation

### Upload PDF
- **URL**: `/upload_pdf`
- **Method**: `POST`
- **Content-Type**: `multipart/form-data`
- **Parameters**: 
  - `file`: PDF file to upload (required)
  - `namespace`: Namespace in Pinecone to store vectors (optional)
- **Response**: JSON with upload status including:
  - `success`: Boolean indicating success
  - `message`: Status message
  - `filename`: Name of the uploaded file
  - `pages_indexed`: Number of pages uploaded to Pinecone (if successful)
  - `indexing_error`: Error message if indexing failed

### Get Response from AI Crew
- **URL**: `/get_response`
- **Method**: `POST`
- **Content-Type**: `application/json`
- **Body**: 
  ```json
  {
    "topic": "Your topic or question here"
  }
  ```
- **Response**: JSON with AI-generated response

## Features

- **PDF Processing**: Uploaded PDFs are automatically:
  - Saved to the knowledge/pdfs directory
  - Processed page by page
  - Converted to embeddings using OpenAI's embedding model
  - Stored in a Pinecone vector database for semantic retrieval

## Structure

- `knowledge/`: Store any knowledge files or data for your agents
  - `pdfs/`: Uploaded PDF files
- `src/my_project/`: Main application code
  - `app.py`: Flask web application
  - `crew.py`: Define your AI crew composition
  - `tools/`: Custom tools for your agents
  - `utils/`: Utility functions
    - `pdf_to_pinecone.py`: PDF processing and Pinecone integration
  - `config/`: Configuration files for agents and tasks

## License

MIT 
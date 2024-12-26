# GEN-AI-PDF-reader-chatboat
# Document Management and Chat System

## Overview
This project is a Flask-based web application designed for efficient document management and query-based interactions. Users can upload PDF documents, which are then processed and indexed using Pinecone for semantic search. The system allows users to ask questions about the content of uploaded documents, leveraging Sentence Transformers for embeddings and Google Gemini for generating responses.

## Features
- **Document Upload**: Upload PDF files to the application.
- **Text Extraction**: Extract text from PDF documents using `PyPDF2`.
- **Semantic Search**: Use Pinecone to index and search document content based on semantic embeddings.
- **Natural Language Queries**: Ask questions about document content and get context-aware answers.
- **Firebase Integration**: Store metadata about uploaded documents.
- **Generative AI Responses**: Generate natural language responses using Google Gemini.
- **Secure and Scalable**: Uses Firebase for secure data storage and Pinecone for scalable indexing.

## Tech Stack
- **Backend**: Flask
- **Database**: Firebase Firestore
- **Search Engine**: Pinecone
- **Text Embedding**: Sentence Transformers
- **Text-to-Vector Model**: `sentence-transformers/msmarco-distilbert-base-v4`
- **Generative AI**: Google Gemini
- **PDF Processing**: PyPDF2
- **Environment Management**: Python `dotenv`

## Prerequisites
- Python 3.8+
- Pinecone API Key
- Firebase Service Account Key
- Google API Key for Generative AI

## Installation

1. **Clone the Repository**:
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **Set Up Virtual Environment**:
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Environment Variables**:
   Create a `.env` file in the root directory and add the following:
   ```env
   PINECONE_API_KEY=your_pinecone_api_key
   FIREBASE_CONFIG={"type": "service_account", "project_id": "your_project_id", ...}
   GOOGLE_API_KEY=your_google_api_key
   ```

5. **Initialize Firebase**:
   - Download the Firebase service account key as a JSON file.
   - Copy the content into the `FIREBASE_CONFIG` environment variable.

6. **Run the Application**:
   ```bash
   python main.py
   ```

   The app will be accessible at `http://localhost:8080`.

## Usage

### 1. Upload a Document
- Navigate to the home page (`/`).
- Upload a PDF file and provide a unique chat name.
- The system will extract text from the PDF and index it in Pinecone.

### 2. Start a Chat Session
- Once the document is uploaded, you'll be redirected to the chat page (`/chat`).
- Ask questions about the uploaded document's content.

### 3. Query the Document
- Use the chat interface to ask questions.
- The application will retrieve relevant content from Pinecone and generate a response using Google Gemini.

## File Structure
```
.
├── main.py                  # Main application script
├── templates/               # HTML templates for Flask
│   ├── upload.html          # Document upload page
│   └── chat.html            # Chat interface
├── static/                  # Static files (CSS, JS, images)
├── requirements.txt         # Python dependencies
├── .env                     # Environment variables
└── README.md                # Project documentation
```

## Key Functions

### Document Processing
- **`extract_text_from_pdf(file)`**: Extracts text from uploaded PDF files.
- **`allowed_file(filename)`**: Validates file type.

### Indexing and Search
- **`index_document(text, chat_name)`**: Splits text into sentences, encodes them, and indexes embeddings in Pinecone.
- **`query_pinecone(index_id, question)`**: Searches the Pinecone index for the most relevant content.

### Chat and Response Generation
- **`generate_response(context, question)`**: Uses Google Gemini to generate a natural language response based on context.

### Metadata Management
- **`store_metadata(chat_name, index_id)`**: Stores document metadata in Firebase.
- **`get_index_id(chat_name)`**: Retrieves the index ID for a given chat name from Firebase.

## Error Handling
- **File Upload**: Validates file presence and type.
- **Indexing**: Ensures embeddings match the correct dimensions and handles batch upserts.
- **Querying**: Validates questions and handles missing or irrelevant data gracefully.

## Deployment
To deploy the application on a production server:
1. Use a production-grade WSGI server like Gunicorn.
2. Set `debug=False` in `app.run()`.
3. Configure HTTPS and secure environment variables.

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.

## Acknowledgments
- [Pinecone](https://www.pinecone.io/)
- [Firebase](https://firebase.google.com/)
- [Sentence Transformers](https://www.sbert.net/)
- [Google Gemini](https://cloud.google.com/generative-ai/)

## Contact
For queries or suggestions, please contact Aman kumar patel at [amanp6659@gmail.com].


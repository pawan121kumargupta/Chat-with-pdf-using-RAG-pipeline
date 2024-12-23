# Retrieval-Augmented Generation (RAG) Pipeline for Chat with Website Content

This project implements a Retrieval-Augmented Generation (RAG) pipeline that allows users to query structured and unstructured data extracted from websites. By integrating web scraping, embeddings, a vector database, and a language model, the system provides accurate, context-rich responses.

---

## features

### 1. **Data Ingestion**
- **Input**: URLs or a list of websites.
- **Process**:
  - Crawl and scrape content from the provided websites.
  - Extract textual content, metadata, and key data fields.
  - Segment content into chunks for granularity.
  - Generate embeddings for chunks using a pre-trained embedding model.
  - Store embeddings in a vector database (FAISS) with metadata for efficient retrieval.

### 2. **Qery Handling**
- **Input**: Natural language questions from users.
- **Process**:
  - Convert the user's query into vector embeddings.
  - Perform a similarity search in the vector database to find the most relevant chunks.
  - Retrieve relevant data for further processing.

### 3. **Response Generation**
- **Input**: Relevant chunks and the user's query.
- **Process**:
  - Use a large language model (LLM) with retrieval-augmented prompts.
  - Generate responses that incorporate retrieved data to ensure factuality and context.

---

## Prerequisites

### Technologies Used
- **Python 3.8+**
- **Libraries**:
  - `beautifulsoup4`: For web scraping.
  - `requests`: For HTTP requests.
  - `pickle`: For saving and loading data.
  - `langchain`: For embeddings, vector stores, and LLM integration.
  - `faiss-cpu`: For efficient vector search and storage.
  - `transformers`: For HuggingFace embeddings.

### Installation
Install the required libraries using pip:
```bash
pip install beautifulsoup4 requests langchain faiss-cpu transformers
```

---

## How It Works

### Step 1: Data Ingestion
1. Enter website URLs when prompted.
2. The system scrapes content from `<p>` tags of the websites.
3. Extracted content is segmented into chunks (chunk size: 1000 characters, overlap: 100 characters).
4. Embeddings are created using the `sentence-transformers/all-MiniLM-L6-v2` model.
5. Embeddings and metadata are stored in a FAISS vector database (`faiss_store_openai.pkl`).

### Step 2: Query Handling
1. Input your question when prompted.
2. The system converts the question into vector embeddings.
3. A similarity search in the FAISS index retrieves relevant content.

### Step 3: Response Generation
1. Relevant content and the user’s query are passed to the `ChatGroq` language model.
2. The LLM generates a context-rich, factual response.

---

## Usage

### Running the Script
1. Execute the script in your terminal:
   ```bash
   python script_name.py
   ```
2. Enter website URLs when prompted:
   ```
   Enter the website URLs (comma-separated): https://example.com, https://another-example.com
   ```
3. Ask a question:
   ```
   Ask a Question: What is the main content of the first website?
   ```
4. Receive the AI-generated response.

---

## Functional Components

### Core Functions
- **`scrape_website(url)`**: Scrapes content from a URL.
- **`process_websites(urls)`**: Processes multiple URLs, generates embeddings, and saves them.
- **`RetrievalQA`**: Combines the FAISS vector retriever and the LLM for accurate responses.

### File Outputs
- **`faiss_store_openai.pkl`**: Serialized FAISS vector database storing embeddings and metadata.

---

## Example Output

### Input URLs
```
https://example.com, https://another-example.com
```

### Scraping and Embedding Creation
```
Processing website: https://example.com
Processing website: https://another-example.com
Embedding Vector Started Building...
Text extracted and FAISS index saved.
```

### Query and Response
```
Ask a Question: What topics are covered on the first website?
Answer:
[The AI-generated response based on the retrieved content]
```

---

## Enhancements for Future Versions

- Add support for scraping additional tags (e.g., `<h1>`, `<table>`).
- Expand to handle non-HTML content (e.g., PDFs, CSVs).
- Introduce a web-based interface for real-time interaction.

---

## License
This project is licensed under the MIT License.



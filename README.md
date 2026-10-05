# 📊 Data Analysis AI Agent

**Streamlit + Gemini + Pinecone**

A Streamlit-based **Retrieval-Augmented Generation (RAG) Data Analysis Agent** that allows users to upload structured and unstructured data, automatically generates insights, indexes the uploaded content, and answers natural-language questions using Gemini-powered RAG.

---

## 🚀 Overview

The **Data Analysis AI Agent** combines data analysis, embeddings, vector search, and generative AI to provide an interactive way to explore uploaded datasets and documents.

The application can:

* 📁 Accept **CSV, Excel, JSON, and PDF** files
* 🤖 Automatically generate **proactive insights** when a file is uploaded
* 🔎 Convert document chunks and table rows into embeddings
* 🧠 Store embeddings in **Pinecone** for semantic retrieval
* 💬 Answer user questions using **RAG + Gemini**
* 📈 Generate data visualizations
* 💡 Suggest relevant follow-up questions
* 📥 Provide a downloadable analysis summary
* 🎛️ Allow users to select the Gemini model for analysis

---

## ✨ Key Features

### 📂 Multi-Format Data Upload

Supports multiple file formats:

| Format          | Supported |
| --------------- | :-------: |
| CSV             |     ✅     |
| Excel (`.xlsx`) |     ✅     |
| JSON            |     ✅     |
| PDF             |     ✅     |

---

### 🔍 Retrieval-Augmented Generation

The application follows a RAG-based workflow:

```text
User Upload
     ↓
File Parsing
     ↓
Data Chunking / Row Processing
     ↓
Gemini Embeddings
     ↓
Pinecone Vector Database
     ↓
User Question
     ↓
Semantic Retrieval
     ↓
Relevant Context
     ↓
Gemini LLM
     ↓
Answer + Insights + Visualization
```

---

### 📊 Proactive Insights

Insights are automatically generated when data is uploaded, without requiring the user to ask a question first.

The insight generation process can identify:

* Statistical summaries
* Outliers
* Trends
* Important patterns
* Potential anomalies
* Relevant characteristics of the uploaded data

---

### 🧠 Vector Search with Pinecone

Uploaded content is transformed into embeddings using **Gemini embedding models** and indexed in Pinecone.

This enables semantic retrieval of relevant:

* Document chunks
* Table rows
* Data points
* Contextual information

The retrieved information is then provided to Gemini to generate grounded answers.

---

### 💬 AI-Powered Data Questions

Users can ask natural-language questions about their uploaded files.

For example:

```text
"What are the main trends in the dataset?"

"Which values appear to be outliers?"

"Summarize the most important findings."

"Which category performed the best?"

"What patterns can you identify in the data?"
```

The RAG pipeline retrieves relevant information before sending the context to Gemini for response generation.

---

### 📈 Visualizations

The application includes visualization utilities for presenting data and analysis results in an easy-to-understand format.

---

### 💡 Follow-Up Questions

After analysis, the application can suggest relevant follow-up questions to help users explore their data further.

---

### 📥 Downloadable Summary

Users can download a summary of the generated analysis and insights for further use.

---

## 🛠️ Tech Stack

| Technology                          | Purpose                             |
| ----------------------------------- | ----------------------------------- |
| **Python**                          | Core programming language           |
| **Streamlit**                       | Web application and UI              |
| **Google Gemini**                   | Generative AI and embeddings        |
| **Pinecone**                        | Vector database and semantic search |
| **RAG**                             | Context-aware question answering    |
| **Pandas**                          | Data processing and analysis        |
| **LangChain-style wrappers**        | Retrieval and RAG logic             |
| **Matplotlib / Plotting Libraries** | Data visualization                  |

---

## 📁 Project Structure

```text
Data-Analysis-AI-Agent/
│
├── app.py
├── parsers.py
├── insights.py
├── indexer.py
├── rag.py
├── gemini_client.py
├── viz.py
├── requirements.txt
│
├── config/
│   └── secrets_template.toml
│
└── .streamlit/
    └── secrets.toml
```

### File Descriptions

| File                           | Description                                                             |
| ------------------------------ | ----------------------------------------------------------------------- |
| `app.py`                       | Streamlit application entry point                                       |
| `parsers.py`                   | File parsing utilities for CSV, Excel, JSON, and PDF                    |
| `insights.py`                  | Generates proactive insights including statistics, outliers, and trends |
| `indexer.py`                   | Handles chunking, embeddings, and Pinecone upserts                      |
| `rag.py`                       | Handles retrieval and RAG-based question answering                      |
| `gemini_client.py`             | Lightweight HTTP wrappers for Gemini generation and embeddings          |
| `viz.py`                       | Plotting and visualization utilities                                    |
| `config/secrets_template.toml` | Template for required API secrets                                       |
| `.streamlit/secrets.toml`      | Local secrets configuration — **must not be committed**                 |
| `requirements.txt`             | Python dependencies                                                     |

---

## ⚙️ Installation & Setup

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd Data-Analysis-AI-Agent
```

### 2. Install Dependencies

Create a virtual environment if desired, then install the required packages:

```bash
python -m pip install -r requirements.txt
```

### 3. Configure API Keys

You need your own:

* **Gemini API Key**
* **Pinecone API Key**

Use the provided secrets template:

```text
config/secrets_template.toml
```

Create or edit:

```text
.streamlit/secrets.toml
```

and add your API credentials according to the template.

> ⚠️ **Never commit real API keys to GitHub.**

### 4. Run the Application

Start the Streamlit application with:

```bash
streamlit run app.py
```

The application will open in your browser.

---

## 🔐 Security

API credentials should always be kept outside the source code.

### Local Development

Store credentials in:

```text
.streamlit/secrets.toml
```

Make sure this file is included in `.gitignore`:

```gitignore
.streamlit/secrets.toml
```

### Streamlit Cloud

For deployment on Streamlit Cloud, add your API keys through the application's **Secrets** configuration instead of committing them to the repository.

> 🚨 **Do not commit actual Gemini or Pinecone API keys to a public repository.**

---

## 🤖 Gemini API Configuration

This project uses a lightweight HTTP wrapper in:

```text
gemini_client.py
```

The wrapper communicates with Google's Generative Language API endpoints for:

* Text generation
* Embeddings

Depending on the Gemini API configuration and models available to your account, you may need to modify:

* API endpoints
* Model names
* Request payload structure
* Embedding configuration

Relevant changes can be made inside:

```text
gemini_client.py
```

Comments in the file indicate where endpoint and model configuration may need to be updated.

---

## 🔄 Application Workflow

```text
                 ┌─────────────────────┐
                 │   Upload File       │
                 │ CSV/XLSX/JSON/PDF   │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │    File Parser      │
                 └──────────┬──────────┘
                            │
              ┌─────────────┴─────────────┐
              ▼                           ▼
     ┌─────────────────┐        ┌──────────────────┐
     │ Data Processing │        │ Proactive        │
     │ & Chunking      │        │ Insights         │
     └────────┬────────┘        └──────────────────┘
              │
              ▼
     ┌─────────────────────┐
     │ Gemini Embeddings   │
     └──────────┬──────────┘
                │
                ▼
     ┌─────────────────────┐
     │ Pinecone Vector DB  │
     └──────────┬──────────┘
                │
                ▼
        ┌───────────────┐
        │ User Question │
        └───────┬───────┘
                │
                ▼
     ┌─────────────────────┐
     │ Semantic Retrieval  │
     └──────────┬──────────┘
                │
                ▼
     ┌─────────────────────┐
     │ Relevant Context    │
     └──────────┬──────────┘
                │
                ▼
     ┌─────────────────────┐
     │ Gemini Generation   │
     └──────────┬──────────┘
                │
                ▼
     ┌─────────────────────┐
     │ Answer + Charts +   │
     │ Follow-up Questions │
     └─────────────────────┘
```

---

## 📌 Requirements

Before running the application, ensure you have:

* Python installed
* A Gemini API key
* A Pinecone API key
* Internet connectivity
* All dependencies listed in `requirements.txt`

---

## 🔮 Future Enhancements

Potential improvements include:

* Support for additional file formats
* Advanced automated data cleaning
* More visualization types
* Conversation memory
* Improved multi-document retrieval
* Advanced filtering and metadata search
* Authentication and user management
* Production-ready deployment
* Enhanced evaluation of RAG responses

---

## 👩‍💻 Author

**Moulika Mallula**

Computer Science & Engineering — Artificial Intelligence & Machine Learning

---

## ⭐ Project Highlights

> **Upload your data → Automatically discover insights → Ask questions → Retrieve relevant context → Get AI-powered answers.**

This project demonstrates the integration of:

**Generative AI + RAG + Vector Databases + Data Analysis + Data Visualization + Streamlit**

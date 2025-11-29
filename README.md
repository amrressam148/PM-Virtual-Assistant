# 🤖 Product Sage: Enterprise AI Assistant (Local RAG)

> **A privacy-first, retrieval-augmented generation (RAG) agent designed to unify scattered product knowledge into a Single Source of Truth.**

---

## 📖 Overview

**Signavio Sage** is a Proof-of-Concept (PoC) AI assistant built to solve the challenge of fragmented internal knowledge. In modern enterprises, critical information is often scattered across Confluence, SharePoint, and Productboard. 

This project demonstrates how a **Local RAG Architecture** can ingest these documents, index them securely, and allow employees to ask natural language questions to retrieve accurate, sourced answers—without data ever leaving the company's infrastructure.

## ✨ Key Features

* **🔒 Privacy-First Architecture:** Runs 100% locally using **Ollama** and **ChromaDB**. No sensitive data is sent to external APIs (OpenAI/Google), ensuring full data sovereignty.
* **🧠 RAG Pipeline:** Implements a full retrieval pipeline: Document Loading → Chunking → Embedding → Vector Storage → Contextual Retrieval.
* **🛡️ Governance & Permissions (RBAC):** Features a simulated **Role-Based Access Control** system.
    * *Sales Users* can only access public documentation.
    * *Product Owners* can access sensitive strategic documents (e.g., "Project Phoenix").
* **✅ Trust & Citations:** Every answer provided by the agent includes a **citation** (source filename) to verify accuracy and reduce hallucinations.
* **🚫 Hallucination Guardrails:** Custom prompt engineering ensures the model refuses to answer questions outside the provided knowledge base (e.g., weather, general trivia).

## 🛠️ Tech Stack

* **Framework:** Python 🐍
* **UI:** Streamlit 🎈
* **Orchestration:** LangChain 🦜🔗
* **LLM & Embeddings:** Ollama (Mistral 7B / all-minilm) 🦙
* **Vector Database:** ChromaDB 💾
* **Document Processing:** LangChain Community Loaders & Unstructured

## ⚙️ Installation & Setup

### Prerequisites

1. **Python 3.11+**
2. **Ollama** installed and running on your machine.

### Steps

1. **Clone the Repository**

   ```bash
   git clone https://github.com/YourUsername/Signavio-Sage.git
   cd Signavio-Sage
   ```

2. **Create a Virtual Environment**

   ```bash
   python -m venv venv
   # Windows (PowerShell):
   .\venv\Scripts\Activate.ps1
   # Mac/Linux:
   source venv/bin/activate
   ```

3. **Install Dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Pull Local Models (via Ollama)**
   
   Make sure the Ollama app is running in the background, then run:

   ```bash
   ollama pull mistral:7b
   ollama pull all-minilm
   ```

5. **Build the Knowledge Base**
   
   Run the ingestion script to create the Vector Database:

   ```bash
   python vector.py
   ```

6. **Run the Application**

   ```bash
   streamlit run app.py
   ```

## 📂 Project Structure

```
├── app.py              # Main application logic (UI & Chat Loop)
├── vector.py           # ETL Pipeline (Ingestion & Embedding)
├── requirements.txt    # Project dependencies
├── data/               # Folder containing knowledge base files
│   ├── onboarding.md
│   ├── roadmapping.md
│   └── project_phoenix.md (Sensitive Data)
└── README.md
```

## 🧪 Usage Scenarios

You can test the **Governance Logic** using the dropdown menu in the sidebar:

1. **Scenario A: Public User (Sales)**
   * *Question:* "What is our roadmapping process?" → **Success** (Returns answer from `roadmapping.md`).
   * *Question:* "What is Project Phoenix?" → **Denied** (Access restriction logic triggers).

2. **Scenario B: Internal User (Product Team)**
   * *Question:* "What is Project Phoenix?" → **Success** (Returns confidential info from `project_phoenix.md`).

## 🔮 Future Roadmap

* **Scalability:** Replace local ChromaDB with a production-grade vector store (e.g., Pinecone or pgvector).
* **Live Data:** Connect to real APIs (Confluence/SharePoint) via Airflow ETL pipelines instead of static Markdown files.
* **Proactive UX:** Integrate as a Slack Bot to proactively surface insights to Product Managers.
* **Evaluation:** Implement RAGAS metrics to automatically test answer accuracy.

## 👤 Author

**Amr Ahmad**

* **Role:** AI & Data Engineering Master's Student
* **Focus:** Building secure, scalable AI products.
* [LinkedIn](https://www.linkedin.com/in/amr-essam-kamaleldin-4506881a9/) | [GitHub](https://github.com/amrressam148)

---

*This project was developed as a technical case study for Product Excellence workflows.*

```mermaid
flowchart LR
    subgraph Storage ["Data Layer"]
        Fabric[Microsoft Fabric OneLake]
    end

    subgraph Pipeline ["Processing Pipeline"]
        AF[Azure Functions]
        DI[Document Intelligence]
    end

    subgraph Search ["Retrieval Layer"]
        AIS[Azure AI Search]
        CDB[Cosmos DB / SQL]
    end

    subgraph Interaction ["AI & User Layer"]
        CS[Copilot Studio]
        LLM[LLM - AI Foundry]
    end

    Fabric --> AF
    AF --> DI
    DI --> AF
    AF --> AIS & CDB
    CS --> AF
    AIS & CDB -- Context --> AF
    AF -- Prompt --> LLM
    LLM -- Response --> CS

  ```



#  End-to-End Explanation

This document outlines the architectural flow for a system.

## 1️⃣ Data Layer
*   **Source of Truth:** All enterprise documents (PDFs, texts, tables) and structured data reside in **Microsoft Fabric (OneLake)**.

## 2️⃣ Processing & Indexing (Offline Pipeline)

*   **Ingestion:** **Azure Functions** fetches data from **Azure Fabric** for processing.
*   **Extraction:** **Azure AI Document Intelligence** extracts text, tables, and structures.
*   **Vectorization:** Content is chunked and converted into embeddings.

  
*   **Storage:** 
    *   Unstructured data is indexed in **Azure AI Search** (utilizing Vector + Keyword search).
    *   Relational or graph-based metadata is stored in **Azure Cosmos DB** or **Azure SQL**.

## 3️⃣ Runtime Query (The RAG Flow)
When a user interacts with the system:

1.  **User Interface:** The user submits a query via **Microsoft Copilot Studio** or a **custom Web App**.
2.  **Orchestration:** **Azure Function**s receives the request.
3.  **Retrieval:** 
    *   The system searches **Azure AI Search** for the most relevant document chunks.
    *   It pulls specific user context or permissions from **Cosmos DB**.
4.  **Augmentation & Generation:** 
    *   The user query + retrieved documents are sent to **Azure AI Foundry**.
    *   **The Large Language Model (LLM)** generates a response strictly grounded in the provided data.
5.  **Output:** A cited, explainable answer is returned to the user.

---


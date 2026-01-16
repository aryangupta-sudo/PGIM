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

```mermaid

flowchart LR

    subgraph Historical Data
        A1[Excel 3Y Data] --> B1[Break Components]
        B1 --> C1[JSON Conversion]
    end

    subgraph SEC Data
        A2[Download 10-K/10-Q PDFs] --> B2[Extract Content]
        B2 --> C2[CSV Conversion]
    end

    subgraph Mapping Layer
        C1 --> D[Universal Mapping]
        C2 --> D
        D --> E[Fill Missing Metrics]
        E --> F[Unified Mapping Output]
    end

    subgraph Validation & Output
        F --> G[QA Validation]
        G --> H[Generate 2025 Excel Template]
    end


    ```

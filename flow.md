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
    end

    D --> I{Mapping Valid?}

    I -->|Yes| Z[Generate 2025 Excel from New 10-K/10-Q PDF]

    I -->|No| E[Run Unified Mapping Pipeline]
    E --> F[Mapping Fixed]
    F --> Z


    ```

# Enterprise AI Platform Architecture

## Overall Architecture

``` mermaid
flowchart TB
    subgraph APP["1. AI Application Layer"]
        direction LR
        A1["Tool Management"]
        A2["Business Management"]
        A3["Trigger Management"]
        A4["System Prompt Management"]
        A5["Knowledge Discovery & Workflows"]
        A6["Agent Framework"]
    end

    subgraph FOUNDATION["2. Common AI Foundation"]
        direction LR
        subgraph RAG["RAG Foundation"]
            R1["Embedding & Vector DB"]
            R2["Full-Text & Hybrid Search"]
            R3["Access Control & Retrieval"]
            R4["Vector Store"]
            R5["Knowledge Storage"]
            R6["Generative Model"]
        end
        subgraph GUARD["AI Guardrails"]
            G1["Orchestrator"]
            G2["Policies"]
            G3["Guardrail Models"]
        end
        subgraph MCP["MCP Gateway"]
            M1["MCP Catalog"]
            M2["Tool Integration"]
            M3["Authentication & Authorization"]
        end
    end

    subgraph MODEL["3. Model as a Service"]
        direction LR
        S1["Model API Catalog Management"]
        S2["Application Management"]
        S3["API Key & Security Management"]
        S4["Authentication & Authorization"]
        S5["Token Usage Limits"]
        S6["External Model Integration"]
        LLM["LLM Providers"]
        S1 --- LLM
        S2 --- LLM
        S3 --- LLM
        S4 --- LLM
        S5 --- LLM
        S6 --- LLM
    end

    subgraph AGENT["4. Agent & Model Platform"]
        direction LR
        E1["Model Catalog"]
        E2["Model Registry"]
        E3["Deployment Management"]
        E4["Inference Engine"]
        E5["Distributed Inference"]
        E6["Inference Performance Evaluation"]
    end

    subgraph FT["5. Fine-Tuning Platform"]
        direction LR
        F1["Data Preparation"]
        F2["Synthetic Data Generation"]
        F3["Distributed Training"]
    end

    APP --> FOUNDATION
    FOUNDATION --> MODEL
    MODEL --> AGENT
    AGENT --> FT

    subgraph OBS["Cross-Layer Operations & Observability (OpenShift)"]
        direction LR
        O1["Model Performance Monitoring"]
        O2["User Feedback"]
        O3["Metrics"]
        O4["Logging"]
        O5["Tracing"]
        O6["GPU Utilization"]
        O7["Token Consumption"]
    end

    OBS -. "Cross-layer monitoring" .-> APP
    OBS -.-> FOUNDATION
    OBS -.-> MODEL
    OBS -.-> AGENT
    OBS -.-> FT

    style APP fill:#eaf2ff,stroke:#3975c6,color:#17365d
    style FOUNDATION fill:#e9f6f1,stroke:#319477,color:#174c3c
    style MODEL fill:#edf0ff,stroke:#6679c9,color:#26366b
    style AGENT fill:#f1edff,stroke:#8870c5,color:#40316d
    style FT fill:#e9f6f1,stroke:#319477,color:#174c3c
    style OBS fill:#fff4e5,stroke:#c58a32,color:#684516
```

## Responsibilities of Each Layer

  -----------------------------------------------------------------------
  Layer                               Primary Responsibilities
  ----------------------------------- -----------------------------------
  1\. AI Application Layer            Development and management of AI
                                      agents and business applications

  2\. Common AI Foundation            Provides shared capabilities such
                                      as RAG, guardrails, and MCP

  3\. Model as a Service              LLM API integration,
                                      authentication, usage limits, and
                                      external model connectivity

  4\. Agent & Model Platform          Model management, deployment,
                                      inference, and performance
                                      evaluation

  5\. Fine-Tuning Platform            Data preparation, synthetic data
                                      generation, and model training

  Cross-Layer Operations              Monitoring, logging, metrics, GPU
                                      utilization, and token consumption
                                      management through OpenShift
  -----------------------------------------------------------------------

## Key Design Principles

1.  **Use OpenShift as the common execution and operations platform.**\
    Rather than managing each AI capability independently, operate them
    through an integrated platform.

2.  **Abstract model consumption through Model as a Service.**\
    Integrate multiple LLM providers so that applications can use models
    without needing to handle provider-specific differences.

3.  **Standardize connectivity to external tools through the MCP
    Gateway.**\
    Centralize the MCP catalog, tool integration, authentication, and
    authorization.

4.  **Prepare for the evolution of AI agents.**\
    Move beyond fixed model selection and consider semantic routing,
    which selects the appropriate model based on factors such as task
    complexity.

---
config:
  layout: elk
---
flowchart LR
 subgraph Inputs["Inputs"]
        A["Emission sensor A"]
        A2["Emission sensor B"]
        B["Operational data"]
        C["Geospatial data"]
        D["Field inspection & repair data"]
        X["Third-party datasets"]
  end
 subgraph subGraph1["Per-output pipelines"]
    direction TB
        FR[("One-off ETL for Regulatory Reports")]
        FG[("One-off ETL for Inventories")]
        FH[("One-off ETL for Emergency Response")]
        FI[("One-off ETL for Repairs/CMMS")]
        FJ[("One-off ETL for Risk/Analytics")]
  end
 subgraph Outputs["Outputs"]
        F["Regulatory reports"]
        G["Regional / Global inventories"]
        H["Emergency responses"]
        I["Repair actions"]
        J["Risk analysis"]
  end
    A --> FR & FG & FH & FI
    A2 --> FR & FG & FJ
    B --> FR & FG & FH & FJ
    C --> FR & FG & FH & FJ
    D --> FR & FG & FI
    X --> FR & FJ
    FR --> F
    FG --> G
    FH --> H
    FI --> I
    FJ --> J
    FR --- R1[["Manual reconciliation"]]
    FG --- R1
    FH --- R2[["Conflicting definitions"]]
    FI --- R2
    FJ --- R3[["Lost metadata"]]
    A2 -.-> M[("Missing / ignored sources")]
    X -.-> M
    M -. data gaps .-> G
    M -. blind spots .-> J
    W["Write mappings N times"] -. note .- FR & FG & FH & FI & FJ
     FR:::etl
     FG:::etl
     FH:::etl
     FI:::etl
     FJ:::etl
     R1:::bad
     R2:::bad
     R3:::bad
     M:::bad
    classDef etl fill:#fff3cd,stroke:#b58900,stroke-width:1px,color:#000
    classDef bad fill:#ffe6e6,stroke:#e3342f,stroke-width:1px,color:#000
    linkStyle 0 stroke-dasharray: 5 5,fill:none
    linkStyle 4 stroke-dasharray: 5 5,fill:none
    linkStyle 7 stroke-dasharray: 5 5,fill:none
    linkStyle 11 stroke-dasharray: 5 5,fill:none
    linkStyle 15 stroke-dasharray: 5 5,fill:none
    linkStyle 18 stroke-dasharray: 5 5,fill:none
    linkStyle 1 stroke-dasharray: 5 5,fill:none

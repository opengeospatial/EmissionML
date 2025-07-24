# OGC EmissionML Discussion Paper — Outline

## 1. Executive Summary *(~0.5 page)*

- Introduce EmissionML and its relevance to the emissions data ecosystem.
- State the purpose of the discussion paper: to educate, clarify, and encourage adoption.
- Highlight benefits for key audiences:
  - **Regulators:** interoperable, auditable, credible data foundation; enabling automated data/calculation verification and audit
  - **Voluntary Reporting Frameworks (e.g., OGMP, MiQ):** semantic integration layer; scalable implementation of the framework; lower adoption curve for operators; enabling automated data/calculation verification and audit
  - **Vendors/Developers:** consistent ontology and data model; faster integration with other systems
  - **Operators:** seamless integration of data from multi-systems and multi-vendors; cheaper and faster root cause analysis, reporting and compliance; minimize delay from detection to repair; prevent vendor lock-in
  - **Investors/ESG stakeholders:** transparency and traceability of emissions data for risk reduction

---

## 2. The Problem: Lacking Consistent Ontology and Fragmentation in Emissions Data *(~0.5 page)*

- Pain points in current ecosystem:
  - High cost to operationalize emissions reduction at scale
  - Time consuming to integrate data from multiple sources and vendors in order to respond to detections and/or predict emissions
  - Difficulty tracing and comparing emissions across sources
  - Emissions estimations, including reconciliation, bottlenecked by poor data integration, consistency, quality, provenance
  - Time consuming and labour intensive to reproduce and audit emissions
  - Vendor lock-in and custom integrations
  - Incompatible reporting formats and templates

- EmissionML addresses these gaps by introducing an international standard-based, future-proof, extensible, and scalable ontology and data model

Using the Geospatial Web as a successful story of data sharing standards allowing us to access geospatial data seamlessly. Information created and shared with OGC standards (e.g., simple features, web tiles). Geospatial Web servers (e.g., ) make information available on the Web (e.g., web maps). Standard-compliant browsers allows users to interact with the web maps and used by billions of people everyday, without even knowing the standards are the enablers that make it happen. EmissionML is a first step to establish the web of information for emission events, observations, and source features, and remove the frictions of emissions data sharing, integration, analysis, and verification.

---

## 3. What EmissionML Is — and What It’s Not *(~1 page)*

### EmissionML **IS**:
- A standardized **ontology and data model**
- A foundation for many **interoperable reporting formats**
- A semantic bridge between **observations**, **source features** and **emission events**
- Designed to enable **AI-ready**, structured, and contextualized data
- Aligned with OGC/ISO/W3C standards for geospatial and observational data

### EmissionML **IS NOT**:
- ❌ A methane MMRV protocol (e.g., MiQ, Veritas)
- ❌ A fixed reporting format (e.g., PDF, CSV schema)
- ❌ An AI or ML model
- ❌ A raw sensor data format
- ❌ A downloadable software tool
- ❌ The only modeling language (it builds on and complements SOSA, O&M, etc.)

> *Source: Based on “What EmissionML Is Not — and Why That Matters”*

---

## 4. Use Cases: Real-World Applications of EmissionML *(~1.5 pages)*

| Title | Stakeholders | Problem | EmissionML Solution | Benefits |
|------------|--------------|---------|----------------------|----------|
| Regulatory or Voluntary Reporting Data Pipeline | Operators, Regulators | Manual formats, vendor lock-in | Emit once → transform to EPA, OGMP, MiQ | Lower compliance cost |
| Cross-Vendor Sensor Integration | Sensor vendors | Proprietary payloads | Normalize via EmissionML | Plug-and-play analytics |
| Super-Emitter Validation | Satellite providers, Regulators | Matching plume to source is hard | Use linked SourceFeatures & Observations | Explainable validation chain |
| Real-Time Operational Response | Control rooms | Fragmented feeds | Normalize events into EmissionML + broker | Faster root-cause triage |
| Carbon-Market Quantification | Offset projects | Hard to verify calculations | Use EmissionML for quant+uncertainty | Higher credit integrity |
| Emissions Simulation | Engineering firms | No model interoperability | Simulators use EmissionML Events | Repeatable, comparable simulation |
| Financial Risk Analysis | Banks, Investors | ESG risk opaque | Load EmissionML into risk models | Risk-based lending, investment decisions |

---

## 5. Adoption Pathways & Call to Action *(~0.5 page)*

- **For Regulators**: design and reference your reporting templates *using* EmissionML
- **For Operators**: manage internal emission data with EmissionML; ask data providers, consultants and software vendors to be EmissionML compliant
- **For Software Vendors**: build EmissionML-compatible data management and software tools to future-proof your platform for regulatory and ESG interoperability
- **For Sensor Providers**: map your observation payloads, procedures, and uncertainties to EmissionML so that simplify integration with customers’ software ecosystems and avoid custom integrations
- **For Investors and ESG Analysts**:  in due diligence ask for EmissionML-tagged data, and visualize/analyze them with EmissionML compliant software tools
- **For Researchers and Academia**: apply EmissionML in research workflows and simulation models; publish interoperable datasets using EmissionML to increase reusability and impact; develop EmissionML open source tools
- **Get Involved**:
  - Visit the [OGC EmissionML GitHub](https://github.com/opengeospatial/EmissionML)
  - Contribute use cases, implementations, or vocabulary feedback
  - Join the OGC Standard Working Group

---

## 6. Appendix *(Optional)*

- **Glossary**: SourceFeature, Observation, Mechanism, EmissionEvent
- **OGC References**:
  - [OGC/ISO O&M 19156:2023](https://www.ogc.org/standards/om/)
  - [W3C SOSA/SSN](https://www.w3.org/TR/vocab-ssn/)
- **Contact**: Join the conversation on GitHub or at the next OGC TC meeting

# EmissionML

**EmissionML** is a free and open [Open Geospatial Consortium](https://ogc.org/) standard ontology and data model for representing and exchanging emission events in a machine-readable, interoperable, and extensible way. It supports multiple emission types, including methane, and aligns with international standards for spatial, temporal, and observational data. EmissionML adheres to the principles of [Findability, Accessibility, Interoperability, and Reusability (FAIR)](https://www.ogc.org/blog-article/how-ogc-contributes-to-fair-geospatial-data/) to ensure long-term utility across scientific, regulatory, and industrial contexts.

---

## About

The purpose of the **OGC Emission Event Modeling Language (EmissionML) Standard Working Group** is to:

- Develop **EmissionML**, an abstract standard for modeling emission events with interoperability and extensibility in mind.
- Build on the EmissionML model to define a **portfolio of open standards** for spatiotemporal emission data sharing and analysis.
  - Example: **MethaneML**, a specialized extension of EmissionML for methane emissions and related observational data.
- Publish new **OGC Best Practices** describing how existing OGC standards can be applied to:
  - Detect emission events
  - Estimate emission quantities

EmissionML is built on existing OGC and ISO standards, including:

- [ISO/OGC 19156 Observation, Measurement, and Sampling (OMS)](https://docs.ogc.org/as/20-082r4/20-082r4.html)
- [W3C/OGC SSN](https://www.w3.org/TR/vocab-ssn/)
- [ISO 19157-1:2023](https://www.iso.org/standard/78900.html)
- [Unified Code for Units of Measure (UCUM)](https://ucum.org/ucum)
- [OGC Abstract Specifications](https://www.ogc.org/standards/abstract-specification/)

---

## Functional Requirements

EmissionML enables:

- **Standardized data sharing** across emission systems and stakeholders
-  **Aggregation** of emission data from heterogeneous sources
-  **Reconciliation** of emissions with built-in support for:
	- Uncertainty modeling
	- Machine readability
	- Provenance
	- Reproducibility
	- Explainability
-  **Georeferencing** with explicit location, geometry, and spatial resolution
-  **Visualization** support with native compatibility for GIS overlays and spatial tools
-  **Flexible reporting** formats that support internal analytics and regulatory adaptation
-  **Built-in provenance** for:
	- Start and end event determination methods
	- Emission quantity estimation method
	- Source feature attribution
-  **Uncertainty modeling** following [ISO 19157](https://www.iso.org/standard/78900.html) for:
	- Event start and end time
	- Quantity of emissions
	- Observation results

---

## Who Should Use EmissionML?

- **Emission Source Operators**  
  Entities responsible for emission-generating facilities or activities. EmissionML enables consistent monitoring, reporting, and compliance workflows.

- **Regulators**  
  Authorities and agencies using EmissionML to analyze and verify emissions across geographies and sectors with full transparency and auditability.

- **Standards and Certification Bodies**  
  Organizations defining frameworks for GHG measurement and verification. EmissionML provides a consistent, extensible data model for reliable certification.

- **Emission Observation Providers**  
  Systems or organizations producing observational or inferred emission data. EmissionML ensures that observational inputs are interoperable with emission records.

- **Emergency Responders**  
  Teams responding to accidental or hazardous emission events. EmissionML enhances situational awareness through spatially and temporally accurate event data.

---

## Contributing

For technical discussions, issue tracking, and schema definitions, please refer to the [GitHub Issues.](https://github.com/opengeospatial/EmissionML).

We hold bi-weekly online meetings to advance the development of the standard and meet in person three times a year at the [OGC Technical Committee meetings](https://www.ogc.org/events/). If you’re interested in participating, please feel free to contact the SWG Chair, [Dr. Steve Liang](https://profiles.ucalgary.ca/hung-ling-steve-liang).

The contributor understands that any accepted contributions may be incorporated into OGC EmissionML standards documents and that all associated copyright and intellectual property rights shall be assigned to the Open Geospatial Consortium (OGC).

The EmissionML Standards Working Group (SWG) at OGC is responsible for the stewardship of the standard. While it maintains formal oversight, the group strives to conduct as much of its work as possible in public.

- [EmissionML Standards Working Group Charter](https://portal.ogc.org/files/108683)
- [Open issues](https://github.com/opengeospatial/EmissionML/issues)

We welcome Pull Requests from contributors. By submitting a Pull Request or commit to this GitHub repository, you agree to the terms outlined in the Observer Agreement. https://portal.ogc.org/files/?artifact_id=92169



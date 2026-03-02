# EmissionML Part 1: Data Model

OGC doc number 25-019

# Standard template

## Content

This folder contains the text for the standard

* `document.adoc` - the main standard document with references to all sections
* `sections/` - each section of the standard document is in a separate document
* `figures/` - figures go here
* `images/` - image files for graphics go here
* `requirements/` - requirements and requirement classes referenced in `clause_7_normative_text.adoc`
* `abstract_tests/` - the Abstract Test Suite comprising one test for every requirement
* `UML/` - UML diagrams

## Building

This standard is built with [Metanorma](https://www.metanorma.org/).

### Prerequisites

Install Metanorma CLI: https://www.metanorma.org/install/

### Build commands

```sh
# Build all output formats (HTML, PDF, DOC, XML)
make all

# Or compile directly
metanorma compile document.adoc
```

Output files are generated as `document.{html,pdf,doc,xml}`.

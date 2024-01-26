# CA-RINF-LDES

This repository contains a [Connector Architecture](https://the-connector-architecture.github.io/site/docs/1_Home)-based workflow definition for producing a [Linked Data Event Stream (LDES)](https://w3id.org/ldes/specification) from the EU Railway Agency's [Registry of Infrastructure](https://rinf.era.europa.eu/RINF/) (RINF) data.

## Connector Architecture workflow for the RINF LDES

The [Connector Architecture](https://the-connector-architecture.github.io/site/docs/1_Home) (CA) allows to declaratively define the set of steps of a (streaming) data processing workflow in the form of an RDF-based document. This document can be taken up by a (set of) CA Runner(s) dedicated to a particular execution environment (i.e., Javascript, Java, Python, Rust, etc), and execute the defined workflow process. Every data transformation step defined in the workflow is declared by instantiating an existing `ca:ProcessClass`, which can be implemented in any programming language as long as there exists a dedicated CA Runner for that language. Communication between processors are defined via instances of `ca:Channel`s.

In this particular case, the workflow's main goal is to transform the original RINF data, which is given in the form of XML documents following the [RINF XSD schema](https://www.era.europa.eu/system/files?file=2022-11/rinf_schema_en.xsd), into a RDF representation of the data, according to the [ERA Vocabulary](https://data-interop.era.europa.eu/era-vocabulary/). Furthermore, the resulting RDF data is targeted to be published in the form of a LDES, which entails creating versioned instances of a predefined set of classes as specified in the data model at hand (i.e., the ERA Vocabulary). A schematic overview of the complete pipeline can be seen next, followed by a detailed description of every step in the workflow.

![Schematic overview](docs/overview.svg)
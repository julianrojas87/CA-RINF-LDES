# CA-RINF-LDES

This repository contains different system components needed for deploying [Connector Architecture](https://the-connector-architecture.github.io/site/docs/1_Home)-based workflows for:

1. Producing and publishing a [Linked Data Event Stream (LDES)](https://w3id.org/ldes/specification) from the EU Railway Agency's [Registry of Infrastructure](https://rinf.era.europa.eu/RINF/) (RINF) data, and;
2. Consuming such LDES for replicating and synchronizing the corresponding Knowledge Graph into a RDF graph store.

A high-level overview of such components can be seen in the following diagram:

![High-level overview](docs/high-level.svg)

For a more detailed description of each component, check each their corresponding README documents:

* [LDES generation pipeline](https://github.com/julianrojas87/CA-RINF-LDES/blob/main/generation-pipeline/README.md)
* [LDES server](https://github.com/julianrojas87/CA-RINF-LDES/blob/main/ldes-server/README.md)
* [LDES consumption pipeline](https://github.com/julianrojas87/CA-RINF-LDES/blob/main/consumption-pipeline/README.md)
* [RDF graph store](https://github.com/julianrojas87/CA-RINF-LDES/blob/main/rdf-graph-store/README.md)

## What is LDES?



## What is the Connector Architecture?

The [Connector Architecture](https://the-connector-architecture.github.io/site/docs/1_Home) (CA) allows to declaratively define the set of steps of a (streaming) data processing workflow in the form of an RDF-based document. This document can be taken up by a (set of) CA Runner(s) dedicated to a particular execution environment (i.e., Javascript, Java, Python, Rust, etc), and execute the defined workflow process. Every data transformation step defined in the workflow is declared by instantiating an existing `ca:ProcessClass`, which can be implemented in any programming language as long as there exists a dedicated CA Runner for that language. Communication between processors are defined via instances of `ca:Channel`s.

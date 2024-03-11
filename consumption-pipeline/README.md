# LDES consumption pipeline

This system component is a [Connector Architecture](https://the-connector-architecture.github.io/site/docs/1_Home)-based pipeline that reads data events from [Linked Data Event Stream (LDES)](https://w3id.org/ldes/specification) and writes them into a target RDF graph store.

In this particular case, we define a pipeline using a CA processor that encapsulates this [LDES client](https://www.npmjs.com/package/ldes-client) implementation, and writes all extracted entity updates into a Virtuoso RDF graph store. Next, a schematic view of this pipeline is shown followed by a description of each processor.

![Schematic overview](../docs/consumption.svg.svg)
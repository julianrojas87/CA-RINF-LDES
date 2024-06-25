# RDF-Connect-RINF-LDES

This repository contains different system components needed for deploying [RDF-Connect](https://rdf-connect.github.io/rdfc.github.io/)-based workflows for:

1. Producing and publishing a [Linked Data Event Stream (LDES)](https://w3id.org/ldes/specification) from the EU Railway Agency's [Registry of Infrastructure](https://rinf.era.europa.eu/RINF/) (RINF) data, and;
2. Consuming such LDES for replicating and synchronizing the corresponding Knowledge Graph into a RDF graph store.

A high-level overview of such components can be seen in the following diagram:

![High-level overview](docs/high-level.svg)

For a more detailed description of each component, check each their corresponding README documents:

* [LDES generation pipeline](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/generation-pipeline/README.md)
* [LDES server](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/ldes-server/README.md)
* [LDES consumption pipeline](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/consumption-pipeline/README.md)
* [RDF graph store](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/rdf-graph-store/README.md)

## What is a LDES?

Linked Data Event Stream (LDES) is a RDF data publishing approach fostered by the EU Semantic Interoperability Community ([SEMIC](https://joinup.ec.europa.eu/collection/semic-support-centre/linked-data-event-streams-ldes)) and officially adopted as a standard specification by the Flemish government through its
[Flemish Smart Data Space project](https://www.vlaanderen.be/vlaamse-smart-data-space-portaal). LDES defines datasets in terms of a collection of immutable objects (aka. members) such as versioned entities or observations, where every member must have its own unique IRI. The main goal of a LDES is to enable efficient replication and synchronization of datasets over the Web. LDES allows data consumers to traverse the collection of members by relying on the [TREE specification](https://w3id.org/tree/specification/) to semantically describe hypermedia relations among subsets or fragments of the data. These hypermedia relations can be configured in multiple ways, e.g. by publishing fragments organized by time or by version. TREE also allows further describing the content of each member by means of a [SHACL](https://www.w3.org/TR/shacl/) shape, which allows data consumers to understand the type and properties of the LDES members.

## What is the RDF-Connect?

[RDF-Connect](https://rdf-connect.github.io/rdfc.github.io/) allows to declaratively define the set of steps of a (streaming) data processing workflow in the form of an RDF document. This document can be taken up by a (set of) RDF-Connect Runner(s) dedicated to a particular execution environment (i.e., Javascript, Java, Python, Rust, etc), and execute the defined workflow process. Every data transformation step defined in the workflow is declared by instantiating an existing `rdfc:ProcessClass`, which can be implemented in any programming language as long as there exists a dedicated RDF-Connect Runner for that language. Communication between processors are defined via instances of `rdfc:Channel`s.

## Run with docker-compose

Each of the system components is independently packaged as a Docker container to allow for deployment flexibility. However, we also provide a `docker-compose` [configuration file](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/docker-compose.yml) that can build and deploy all the components in an integrated manner.

To execute the integrated system, make sure to provide at least the following configuration parameters:

1. Set a user and password for the MongoDB data store in the [environment parameters](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/docker-compose.yml#L7) of the docker-compose file.
2. Make sure the credentials defined for MongoDB are used by both the generation pipeline and the LDES Server. For this, set the following MongoDB connection string in RDF-Connect descriptors of the generation pipeline ([here](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/generation-pipeline/rdfc-pipeline.ttl#L431) and [here](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/generation-pipeline/rdfc-pipeline-init.ttl#L437)) and in the [configuration file](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/ldes-server/config-ldes.json#L125) of the LDES Server:

    ```bash
    mongodb://root:example@mongodb:27017/rinf-ldes?authSource=admin
    ```

3. For the generation pipeline, choose between the [init RDF-Connect pipeline](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/generation-pipeline/rdfc-pipeline-init.ttl) (i.e., the one that transforms and ingest the [initial set of data sources](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/tree/main/generation-pipeline/rawdata/RINF_init) included in this repository) or the [reactive pipeline](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/generation-pipeline/rdfc-pipeline.ttl) that only transforms data sources that are pushed towards it. Configure this [here](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/docker-compose.yml#L24), by setting either `rdfc-pipeline-init.ttl` or `rdfc-pipeline.ttl`.
4. Set the [LDES base URL](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/main/docker-compose.yml#L33) that will be used by the LDES Server.

More granular configuration alternatives are possible for each system components. See the documentation of each components for more information.

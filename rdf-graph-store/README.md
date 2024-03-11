# RDF graph store

This system component represents a SPARQL-compliant RDF graph database. In this particular example, we provide a docker container configuration for a [Virtuoso open source](https://github.com/openlink/virtuoso-opensource) instance.

## Configure update permissions
⚠️Warning⚠️: For this demonstrator, we allow full unrestricted SPARQL UPDATE permission to a particular named graph. However, for production deployments, proper security and access control configurations should be made. See [the documentation](https://docs.openlinksw.com/virtuoso/rdfsparqlprotocolendpoint/#rdfsupportedprotocolendpointurisparqlauthex) for Virtuoso.



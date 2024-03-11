# RDF graph store

This system component represents a SPARQL-compliant RDF graph database. In this particular example, we provide a docker container configuration for a [Virtuoso open source](https://github.com/openlink/virtuoso-opensource) instance.

## Run with Docker

To run Virtuoso open source with Docker, execute the following commands:

```bash
docker pull openlink/virtuoso-opensource-7
```

```bash
docker run --name virtuoso-os --env DBA_PASSWORD=dba -p 1111:1111 -p 8890:8890 -v `pwd`:/database openlink/virtuoso-opensource-7:latest
```

Make sure to set an appropriate `DBA_PASSWORD`.

## Configure update permissions

**⚠️Warning⚠️**: For this demonstrator, we allow full unrestricted SPARQL UPDATE permission over all named graphs. However, for production deployments, proper security and access control configurations should be made. See [the documentation](https://docs.openlinksw.com/virtuoso/rdfsparqlprotocolendpoint/#rdfsupportedprotocolendpointurisparqlauthex) for Virtuoso.

1. Login with your `dba` credential on `http://{your_virtuoso_address}/conductor`.
2. Navigate to `Database` > `Interactive SQL`.
3. Execute the following command to authorize update operations for all named graphs:

    ```SQL
     DB.DBA.RDF_DEFAULT_USER_PERMS_SET ('nobody', 7);
    ```

4. Navigate to `System Admin` > `User Accounts` > `Users` and edit the `SPARQL` user. Add the `SPARQ_UPDATE` account role and click on save.

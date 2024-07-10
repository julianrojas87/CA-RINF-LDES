# LDES Server

This system component provides a container with an implementation of a LDES server. The implementation used by this component is available at <https://github.com/rdf-connect/LDES-Solid-Server>.

## Run with Docker

First make sure that the proper data store address is added in the [server configuration](https://github.com/rdf-connect/RDF-Connect-RINF-LDES/blob/8d55e2876526ff63bd65a2d40951dd05b4d7fd50/ldes-server/config-ldes.json#L125). For example:

```yaml
mongodb://your_user:your_password@localhost:27017/rinf-ldes?authSource=admin
```

Now build the server image as follows:

```bash
docker build -t ldes-server .
```

Finally, run a container of the server with the following command:

```bash
docker run -p 3000:3000 --name ldes-server ldes-server -b {SERVER_ADDRESS}
```

Replace `{SERVER_ADDRESS}` for the URL where the server is reachable, e.g,. <http://localhost:3000>.

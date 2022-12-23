# couch-with-metrics

Example Docker Compose configuration for setting up a CouchDB instance wired up to a Prometheus instance for metrics collection.

The goal of this project is to provide an easy way to evaluate and experiment with CouchDB metrics on Prometheus.

## Usage

### Running

```bash
mkdir prometheus/data
docker compose up -d
```

This will start a CouchDB instance available at `http://localhost:5984` and a Prometheus instance available at `http://localhost:9090`.

### Stopping

To stop the instance and clear all the data, run:

```bash
docker compose down
sudo rm -rf couch
sudo rm -rf prometheus/data
```

### Seeing metrics

Prometheus has a basic web interface at http://localhost:9090/ that allows for running queries and viewing simple graphs.  For example, [this page](http://localhost:9090/graph?g0.expr=couchdb_database_doc_count%7Bdb_name%3D~%22medic%22%7D&g0.tab=0) should show the number of documents in the `medic` database.

To see what CouchDB metrics are available to be queried, visit http://localhost:9984/metrics.    

See the [Prometheus Documentation](https://prometheus.io/docs/prometheus/latest/querying/basics/) for more information on how to write queries.

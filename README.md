# couch-with-metrics

Example Docker Compose configuration for setting up metrics collection for a Couch database using Prometheus.

The goal of this project is to provide an easy way to evaluate and experiment with CouchDB metrics on Prometheus.

## Usage

Two separate usage flavors are supported.  

The [`docker-compose.with-couch.yml`](./docker-compose.with-couch.yml) configuration can be used to start a local CouchDB instance (along with the required Prometheus and exporter services).  

The [`docker-compose.external-couch.yml`](./docker-compose.external-couch.yml) configuration can be used to start the Prometheus and exporter services connected to an existing Couch (or CHT) instance.  _(A typical CHT deployment will technically not allow direct access to the Couch database. Instead, all requests will be filtered through the CHT API. The provided external configuration supports collecting the Couch metrics through the CHT API.)_

### Running

First, cop `dist-env` to a file called `.env`. Then, configure the Couch user (and instance, if connecting to an external database) in the [`.env`](./.env) file.  Then, run the following command to start the services:

```sh
mkdir prometheus/data
docker compose -f docker-compose.*flavor*.yml up -d
```

This will start a Prometheus instance available at `http://localhost:9090`. (If starting a local Couch instance, it will be available at `http://localhost:5984`.)

### Stopping

To stop the instance and clear all the data, run:

```sh
docker compose -f docker-compose.*flavor*.yml down
sudo rm -rf couch
sudo rm -rf prometheus/data
```

### Seeing metrics

Prometheus has a basic web interface at http://localhost:9090/ that allows for running queries and viewing simple graphs.  For example, [this page](http://localhost:9090/graph?g0.expr=couchdb_database_doc_count%7Bdb_name%3D~%22medic%22%7D&g0.tab=0) should show the number of documents in the `medic` database.

To see what CouchDB metrics are available to be queried, visit http://localhost:9984/metrics.    

See the [Prometheus Documentation](https://prometheus.io/docs/prometheus/latest/querying/basics/) for more information on how to write queries.

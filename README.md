# Prometheus Connect Example

In this example we have kafka connect, jmx exporters, prometheus and grafana. What it shows is how to setup kafka connect workers with a prometheus jmx exporter, collect the metrics and display them using grafana.  As part of the example connectors can be created to produce load and some JMX data that is more interesting than nothing.

## Requirements

To run this example you must have the following:
 - must be using a bash shell
 - docker is installed
 - docker-compose is installed

## Running

To start the example run `docker-compose up -d`.
This starts kafka, zookeeper, schema registry, connect workers, jmx exporters, prometheus and grafana.

Once running go to http://localhost:3000 to see the grafana dashboard.

## Connectors

Now that it's running install the file connector like so:

``` connect/connector-install connect/file-connectors/ ```

It should create a topic and submit the connector to one of the connect workers API endpoints via curl. Running it again does not cause issues.

At this point you can run this command to create some sample data for the connectors:

```for i in $(seq 1 6000); do echo "This is message $i" >> connect/file-connectors/source-data/test.txt && sleep 0.1;done ```

That command will produce lines into the test.txt file which the file source connector is reading.

Now look into the connect/file-connectors/sink-data/test.txt and you should see those same lines as they are written by the file sink connector.

## Grafana

Once running go to http://localhost:3000 and check out the confluent dashboard.
There you will see many of the connect JMX metrics mapped out.
Try adding some connectors.

```
connect/connect-install connect/file-connectors
```

```
connect/connect-install connect/datagen
```

The dashboards should update with new data about the connector connectors and their tasks.



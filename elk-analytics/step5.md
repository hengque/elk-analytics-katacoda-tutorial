<p></p>

## Displaying our data in Kibana

Now it's nearly time to start Kibana, where we will see our data. First, to make sure the ELK stack is up and running, open a new terminal tab, choose `Select port to view on Host 1`, and enter port 9200. This is the endpoint that Elasticsearch is hosted at.

The credentials are:
* username: elastic
* password: changeme

If the ELK stack is up and running, you should see a message similar to this one:

```
{
  "name" : "a2bfd2347be4",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "-263ZkthSlevB6I5oyiVoA",
  "version" : {
    "number" : "7.12.0",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "78722783c38caa25a70982b5b042074cde5d3b3a",
    "build_date" : "2021-03-18T06:17:15.410153305Z",
    "build_snapshot" : false,
    "lucene_version" : "8.8.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

(If Kibana ever gives you trouble, it's worth to do this process again to make sure that Elasticsearch is up)


Iaf, berättar hur man klickar runt i Kibana för att skapa index-pattern:et `logstash-*` och ser datan dyka upp i 'Discover'-delen (och påpeka att de är sorterade "äldst överst" så man får scrolla ner för att se det senaste). Gör användaren uppmärksam på 'fälten' (betona att det är ett betydelsefullt ord på något sätt) i panelen nere till vänster, och tipsa om att titta runt lite.

Sen är det dags att använda logstash för att göra datan mer användbar och skapa nya fält. Det ska vi göra i nästa steg.
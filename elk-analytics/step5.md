<p></p>

## Kom på ngn bra titel här

När allt har byggt klart är det dags att öppna Kibana.

Då har vi antingen predefined tabs för Kibana (och ev. Elasticsearch), eller så säger vi till dem att öppna en ny och välja port själva (5601 och ev. 9200). Påpekar credentials (elastic och changeme).

Påpekar också att man kan gå in på 9200 först för att se att det funkar, ska se något i stil med:

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

(och om Kibana någonsin bråkar är det värt att gå in på ES först och se om det är uppe)

Iaf, berättar hur man klickar runt i Kibana för att skapa index-pattern:et `logstash-*` och ser datan dyka upp i 'Discover'-delen (och påpeka att de är sorterade "äldst överst" så man får scrolla ner för att se det senaste). Gör användaren uppmärksam på 'fälten' (betona att det är ett betydelsefullt ord på något sätt) i panelen nere till vänster, och tipsa om att titta runt lite.

Sen är det dags att använda logstash för att göra datan mer användbar och skapa nya fält. Det ska vi göra i nästa steg.
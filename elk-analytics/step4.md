<p></p>

## Configuring the ELK stack

Koppla tillbaka till logstash som hämtar data från flera ställen via logstash.conf. Be användaren öppna filen. Visa att från docker-elk har vi redan två input-ställen (förklara dem kort, gör Beats-återkoppling). Säg att vi vill även ha från vår fil. Lägg till (gör ev. om rutan senare till en som automatiskt kopierar till clipboard; men kanske inte dock för jag kan tycka att sådana är lite störiga ibland):

```
file {
	path => "/usr/share/logstash/logfile.log"
}
```

Påpeka att ELK körs i containers, så vi måste mappa in vår loggfil. Ändra i docker-compose.yml i logstash-delen:

(efter rad 42)
```
- type: bind
    source: /root/logs/spring.log
    target: /usr/share/logstash/logfile.log
```

Sen kör man docker-compose:

`docker-compose up`{{execute}}

Berätta att det kan ta ett tag, och att man kan gå vidare till nästa steg sålänge.
Berätta också att den är uppe när terminalen börjar "spout out messages from kibana_1 and elasticsearch_1" (typ)
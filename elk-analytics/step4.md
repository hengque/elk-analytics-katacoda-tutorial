## Configuring the ELK stack

Koppla tillbaka till logstash som hämtar data från flera ställen via logstash.conf. Be användaren öppna filen. Visa att från docker-elk har vi redan två input-ställen (förklara dem kort, gör Beats-återkoppling). Säg att vi vill även ha från vår fil. Lägg till:

```
file {
	path => "/usr/share/logstash/logfile.log"
}
```

Påpeka att ELK körs i containers, så vi måste mappa in vår loggfil. Ändra i docker-compose.yml i logstash-delen:

(efter rad 42)
- type: bind
    source: /root/logs/spring.log
    target: /usr/share/logstash/logfile.log

TBC
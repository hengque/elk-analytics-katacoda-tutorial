<p></p>

## Summary

We have seen how to use the ELK stack for log management. With Logstash, we ingested data from a log-file, parsed the messages to tag them with various labels, and sent the data on to Elasticsearch. With Kibana, we were able to browse that data, and create visualizations based on the labels Logstash added.

We also discussed how log management tools are helpful to aggregate log messages from large applications, and especially from distributed applications. By now, you hopefully have an appreciation for why these tools can be useful.

Suffice it to say, however, we have only scratched the surface of what is possible with tools like the ELK stack. We only read data from a file, but you can also ingest data from things like Github webhooks, Twitter feeds, SQLite databases, [and more](https://www.elastic.co/guide/en/logstash/current/input-plugins.html). Apart from sending data to Elasticsearch, you can send it in email, to HTTP(S) endpoints, to databases like MongoDB and Redis, and even other monitoring tools (such as Datadog).

The containerized version of the ELK stack used in this tutorial (repo [here](https://github.com/deviantony/docker-elk)) is a simple and useful starting-ground for doing your own experiments with this powerful technology stack. Having completed this tutorial, we hope you feel well-equipped to venture forth on your own and discover even more of what is possible.

Good luck, and thanks for sticking with us to the end!
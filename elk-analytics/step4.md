<p></p>

## Configuring Logstash

We have learned that Logstash is a data-processing pipline that:
* takes in data from multiple sources
* performs transformations on/parses this data
* outputs the result to several different destinations

This three-step process is handled in the `logstash.conf` file in the `docker-elk/logstash/pipeline` folder. Navigate to this file and open it in the editor, or click this link to automatically open it in the editor:
`docker-elk/logstash/pipeline/logstash.conf`{{open}}

Each of the three steps are handled by so-called *plugins*. The first step uses *input plugins*, the second uses *filter plugins*, and the third uses *output plugins*.

<details>
<summary>Logstash plugins</summary>

<div style="display: block;
  margin-left: 10px;
  margin-right: 10px;
  background-color: aliceblue;
  padding: 1em;">
There is a large amount of plugins available in Logstash. With them, you can receive data from a wide variety of sources (see <a href="https://www.elastic.co/guide/en/logstash/current/input-plugins.html">this</a> list of supported input plugins), parse and transform it in various ways (see <a href="https://www.elastic.co/guide/en/logstash/current/filter-plugins.html">this</a> list of supported filter plugins) as well as send the data on to many different destinations (see <a href="https://www.elastic.co/guide/en/logstash/current/output-plugins.html">this</a> list of supported output plugins).

</div>

</details>

The maintainers of `docker-elk` have already added some configuration for us. Within the `input {}` curly brackets we see two input plugins (i.e. data sources from which Logstash will pull data):

* *Beats* is another tool from the people behind the ELK stack, and can be thought of as a more light-weight version of Logstash. We will not be using it in this tutorial.
* Data sent over TCP at port 5000 will be consumed by Logstash. This is useful for manual debugging purposes, and also enables services on other devices to send data over the network.

In the input step, we also want to tell Logstash to pull data from our log file. To do this, we will add the *file plugin*.

```
file {
	path => "/usr/share/logstash/logfile.log"
}
```{{copy}}
*(Tip: You can click the box to copy the content!)*

Since our ELK stack is running in containers, we need to map the "outside" of the containers to the "inside". This is done in the configuration file for `docker-compose`, called `docker-compose.yml`.

Open `docker-elk/docker-compose.yml`{{open}} and add the following under the `volumes` attribute in the `logstash`-part of the file (i.e. after line 42):

```
- type: bind
    source: /root/logs/spring.log
    target: /usr/share/logstash/logfile.log
```{{copy}}

Now we are finally ready to start the stack. Make sure you are in the `docker-elk` in the terminal, and execute:

`docker-compose up`{{execute}}

This can take some time, and you are encouraged to move to the next step as things are starting. Note that the stack is not yet up and running when you see:

```
$ docker-compose up
Starting docker-elk_elasticsearch_1 ... done
Starting docker-elk_logstash_1      ... done
Starting docker-elk_kibana_1        ... done
```

Even though the `done`-messages are there, the stack is – in fact – not yet running.

You will know the stack is up and running when the terminal outputs lots of messages from `kibana_1` and `elasticsearch_1`.
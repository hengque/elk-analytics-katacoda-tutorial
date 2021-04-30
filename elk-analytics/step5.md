<p></p>

## Displaying our data in Kibana

Now it's nearly time to visit and configure Kibana, where we will see our data. First, to make sure the ELK stack is up and running, open Elasticsearch by clicking the `Elasticsearch` terminal tab. This terminal tab is configured to visit our localhost on port 9200. This is the endpoint that Elasticsearch is hosted at.

If it just says "Connecting to Port 9200", it means Elasticsearch is not up and running yet. Try it again after about 30-60 seconds, and it will work.

The credentials are:
* username: `elastic`{{copy}}
* password: `changeme`{{copy}}

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

Assuming the stack is up and running, you should be able to visit Kibana by clicking the `Kibana` terminal tab (the credentials are the same). This tab is configured to access localhost on port 5601, which is the default port for Kibana.

The first time you visit Kibana you will get a "Welcome" landing page with the choice between "Add data" and "Explore on my own". Choose the latter.

<!-- Kanske lägg in bild på startsidan här, lade en bild under assets/kibana-startpage.png -->

Then, open the hamburger menu (three horizontal dashes) in the top left and click on `Discover` under `Analytics`. If your data pipline is correctly setup, the page will say that you have data in Elasticsearch, and that you should create an index pattern. Click the `Create index pattern` button and enter `logstash*`{{copy}} into the index pattern name. It should say that your index pattern has matches in a green box below. Continue to the next step, and choose the timefield `@timestamp` from the dropdown menu. Then, click the `Create index pattern` button.

Once again, expand the hamburger menu at the top left and click on `Discover` under `Analytics`. To the right of the search bar, click the calendar icon and update the timeframe to something more than 15 minutes (for example 15 hours) to ensure that all data you have generated is encompassed within your chosen timeframe (don't forget to click `Apply`).

If everything is working, you will now see all the log messages generated so far.

In the scrollable panel to the left you have `Available fields`, where you can see all the attributes that are available for your data. As we have not yet filtered our messages in Logstash, you will only see the default fields that were extracted automatically for us. The `message` field will contain the actual contents of our log messages, and this is something we'll use in the next step.

Have a look around the UI, if you want, and when you are ready we will proceed to the next step, where it's time to use Logstash to make our data more useful and create more fields.
<p></p>

## Parsing our log messages with Logstash

First, shut down the ELK stack (<kbd>Ctrl</kbd>+<kbd>C</kbd>) in `Terminal 2` and close your Kibana browser window. Then, open `logstash.conf` (it should still be open as a tab in the editor view).

It's time to add our own filters. For this, we will use a *filter plugin* called the *grok plugin*. You can think of it as a *regex*-ish parser. We'll write *grok patterns* that will match our messages and extract values into fields (these will be added to the fields you saw in Kibana in the previous step).

<!--
En aside om grok-plugin, länka till https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html och http://grokdebug.herokuapp.com/

Ge ett bra exempel på hur grok arbetar för att dela upp text i olika 'fält' (som sedan dyker upp i Kibana, återigen är detta ett betydelsefullt ord).

-->

Copy the following contents (remember you can click the box), and add them between the *input plugins* and the *output plugins* in `logstash.conf`:

```
## Add your filters / logstash plugins configuration here
filter {
  if [message] =~ "\tat" {
    grok {
      match => ["message", "^(\tat)"]
      add_tag => ["stacktrace"]
    }
  }
  
  grok {
    match => [ "message",
               "%{TIMESTAMP_ISO8601:time}\s*%{WORD:log_level} %{NUMBER:pid} --- .+? :\s+(?<logmessage>.*)"
             ]
  }

  grok {
    match => [ "logmessage",
               "Greeted: %{WORD:greeted}"
             ]
  }

  ## TODO Henrik, calculator grok

}
```{{copy}}

TODO: Lägg till en details-miljö här där vi skriver om syntaxen lite grann.

If the base application is not running (check the first terminal tab, `Terminal`), now is the time to start it again. Then, in `Terminal 2`, start the ELK stack once again:

`docker-compose up`{{execute T2}}

(Don't forget that the stack is not up and running until the terminal starts emitting lots of messages from `elasticsearch_1` and `kibana_1`. You can check the `Elasticsearch` tab to see if the stack is up and running)

Now, open the `Kibana` terminal tab and go back to the `Discover`-section. You will see your old log messages from before. Since they were emitted before we added the grok filtering rules, they will not have the new fields.

Therefore, you need to trigger the base application to emit some log messages. Generate some errors in the `/generate-errors`-endpoint, exend some greetings in the `/greeting`-endpoint, and show off your math skills in the `/calculator`-endpoint.

After some log messages appear (you can check `Terminal` to verify that they do), hit the blue `Refresh` button in Kibana, and they should appear there as well. Notice that our newly added fields have appeared, both on the messages in the long list, as well as in the panel to the left with `Available fields`.

If you have used the calculator you might see fields such as `calc_divisions`, or `calc_result`. By clicking on one of these fields you can see how many times they have appeared in your data, and with what values.

<!-- Möjligen märkligt att använda 'final' här, eftersom vi kommer ha ett som heter 'finish' efter det. Men på det sista steget kommer vi väl egentligen inte göra något mer än att sammanfatta och ha ngt take-home message, så jag tycker det funkar -->

In the next and final step, we will use the `Dashboard` functionality of Kibana to create some data visualizations based on our data.
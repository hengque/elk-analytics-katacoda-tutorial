<p></p>

## Parsing our log messages with Logstash

First, shut down the ELK stack (<kbd>Ctrl</kbd>+<kbd>C</kbd>) in `Terminal 2` and close your Kibana browser window. Then, open `logstash.conf` (it should still be open as a tab in the editor view).

It's time to add our own filters. For this, we will use a *filter plugin* called the *grok plugin*. You can think of it as a regex-ish parser. We'll write *grok patterns* that will match our messages and extract values into fields (these will be added to the fields you saw in Kibana in the previous step).

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

  grok {
    match => {
      "message" => [
                "Times (?<calc_request>(post)|(get))(t)?ing (to )?calculator: ",
                "(?<calc_expr_validity>((Inv)|V)alid) expression", 
                "(?<calc_expr_validity>Division by zero!)",
                "Additions: (?<calc_additions>[0-9]+)",
                "Subtraction: (?<calc_subtraction>[0-9]+)",
                "Multiplications: (?<calc_multiplications>[0-9]+)",
                "Divisions: (?<calc_divisions>[0-9]+)",
                "Resulting value: (?<calc_result>[0-9\.]+)"
      ]
    }
  }
}
```{{copy}}

<details>
<summary>Grok syntax</summary>

<div style="display: block;
  margin-left: 10px;
  margin-right: 10px;
  background-color: aliceblue;
  padding: 1em;">
<!-- TODO: Inte säker på vad skillnaden är på att ha flera groks och att bara lista flera alternativ inne i en, och inte heller säker på saker som match => "message" :/ 
Vidare vet jag inte om man kallar det control signals 

Sen också, visst för att denna logiskt borde ligga här, men man skulle vilja att användaren startar elk-stack på nytt innan hen läser detta egentligen. Borde vi därför flytta detta längre ner?
TODO Andreas: läs denna kommentar igen när resten är fixat -->

The output from Logstash is `json` data that we forward to Elasticsearch. With the help of the grok plugin we can modify what (key, value)-pairs are included in our resulting `json` objects.</br>
</br> 
In each instance of the grok plugin we specify what we want the received "message":s to match with. This is done in an array in which each element is a regex-like string. Within each of these strings we can define patterns that will match the messages and add a key-value pair to our output json, given that the string matches the pattern.</br>
</br>
For example, the array-element
<code>Greeted: %{WORD:greeted}</code> will match input that contains exactly <code>Greeted: </code> followed by an arbitrary word (WORD is one of ~120 predefined grok patterns, you can see their definitions [here](https://github.com/logstash-plugins/logstash-patterns-core/blob/master/patterns/ecs-v1/grok-patterns)).</br>
</br>
This will create a pair in our `json` output with the key "greeted" and the value of whatever word was matched (in other words, the string pattern essentially means: <code>${VALUE:key}</code>). So, a log-message of "Greeted: World" would create the key-value pair `(greeted, "World")`.</br>
</br>
There is also syntax that lets us [define our own critera for matching](https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html#_custom_patterns), instead of using predefined ones such as "WORD". To do this, we write `(?<field_name>the pattern here)`.</br>
</br>
For example, the string <code>Additions: (?<calc_additions>[0-9]+)</code> will match a string containing <code>Additions: </code> followed by an arbitrary sequence of numbers, and will create a pair with the key "calc_additions" and the value of the number sequence. So, a log-message of "Additions: 42" would create the key-value pair `(calc_additions, 42)`.</br>
</br>
You can read more about grok <a href="https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html ">here</a>. To help you debug your grok strings, <a href="https://grokdebug.herokuapp.com/">here</a> is a tool that lets you enter a grok string and some input to see if there is a match.

</div>

</details>

If the base application is not running (check the first terminal tab, `Terminal`), now is the time to start it again (`./mvnw spring-boot:run`{{execute T1}}). Then, in `Terminal 2`, start the ELK stack once again:

`docker-compose up`{{execute T2}}

(Don't forget that the stack is not up and running until the terminal starts emitting lots of messages from `elasticsearch_1` and `kibana_1`. You can check the `Elasticsearch` tab to see if the stack is up and running)

Now, open the `Kibana` terminal tab and go back to the `Discover`-section. You will see your old log messages from before. Since they were emitted before we added the grok filtering rules, they will not have the new fields.

Therefore, you need to trigger the base application to emit some log messages. Generate some errors in the `/generate-errors`-endpoint, exend some greetings in the `/greeting`-endpoint, and show off your math skills in the `/calculator`-endpoint.

After some log messages appear (you can check `Terminal` to verify that they do), hit the blue `Refresh` button in Kibana, and they should appear there as well. Notice that our newly added fields have appeared, both on the messages in the long list, as well as in the panel to the left with `Available fields`.

If you have used the calculator you might see fields such as `calc_divisions`, or `calc_result`. Most messages (apart from Java exceptions) should also have `log_level` fields that indicate if they were `INFO` messages or `ERROR` messages. The `greeted` field includes the name of the greeted person.

By clicking on one of these fields you can see how many times they have appeared in your data, and with what values.

In the next and final step, we will use the `Dashboard` functionality of Kibana to create some data visualizations based on our data.
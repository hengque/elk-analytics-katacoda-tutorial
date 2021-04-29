<p></p>

## Introducing: The ELK stack

It will take some time to fetch and build the containers (containers are briefly explained below) needed to get the ELK stack up and running. Therefore, the next commands will clone the stack and invoke `docker-compose` (also explained below) to let it set up while you read the information about ELK as the stack is initializing.

First, make sure you go back to the `/root`-folder. This is done because the tutorial assumes both `gs-serving-web-content` and `docker-elk` are in the `/root` folder.

`cd /root`{{execute}}

Next, clone the repo, enter the new folder, and invoke `docker-compose` to build the containers.

`git clone https://github.com/deviantony/docker-elk.git`{{execute}}

`cd docker-elk`{{execute}}

`docker-compose up --no-start`{{execute}}

<details>
<summary>Containers and docker-compose</summary>

<div style="display: block;
  margin-left: 10px;
  margin-right: 10px;
  background-color: aliceblue;
  padding: 1em;">
A <i>container</i> consists of an application and everything that application needs to run, in terms of dependencies, needed system configurations, and so on. Containerization is a useful way of shipping software to make sure they can be run anywhere, assuming software capable of running the containers are available.</br>
</br>
In this tutorial, we are using <code>docker-compose</code> (pre-installed in our Katacoda environment) to start three containers; one containing Elasticsearch, one containing Logstash, and one containing Kibana. The <code>--no-start</code>-flag passed to <code>docker-compose</code> is used to make it build the containers without starting them (we will want to make some configurations before we start).</br>
</br>
You can read more about <code>docker-compose</code> <a href="https://docs.docker.com/compose/reference/">here</a> (and specifically about <code>docker-compose up</code> <a href="https://docs.docker.com/compose/reference/up/">here</a>).

</div>

</details>

There are various ways to run the ELK stack. You can:
* [install](https://www.elastic.co/downloads/) the tools separately and configure them yourself
* use the [hosted ELK service](https://www.elastic.co/cloud/elasticsearch-service/signup?baymax=rtp&storm=whatis-all&elektra=whatis-elkstack)
* run a containerized version where everything is "connected" already

For simplicity's sake, we have chosen the third option by using a Github repository (the `docker-elk` repo you cloned above) that already contains the needed software and configurations. This will allow us to setup the stack quickly and actually focus on using its features.

## Why log management?

At this point, it might be good to motivate why we even need log management tools like the ELK stack. The answer is that these tools are highly useful whenever searching and aggregating log data from applications is of interest. This can provide useful insights for managing an application by e.g. showing where crashes are most likely to occur, or showing how users are interacting with your application.

Without log management tools like the ELK stack, the process of writing custom scripts to scan extensive log outputs of large applications can be daunting. This task is further complicated in the setting of distributed applications (i.e. applications running on several computers, connected via a network) where logs end up in different places. Applications implemented using the *microsevices architecture* are often quoted as being especially benefitted from log management tools.

## A closer look at the ELK stack

<!-- As mentioned, the ELK stack consists of Elasticsearch, Logstash, and Kibana. In the coming steps, we will:
* use Logstash to:
    * pull log messages from our `spring.log` file
    * parse the messages to tag different parts of them (timestamps, log-levels, pid, actual message, etc.)
    * send the data to Elasticsearch
* use Elasticsearch as a data repository containing the data it received from Logstash
* use Kibana ... testar en annan approach här nere: -->

As mentioned, the ELK stack consists of Elasticsearch, Logstash, and Kibana. In the coming steps, we will use Logstash to pull log messages from our `spring.log` file. Then, configure Logstash to parse the messages and tag different parts of them (timestamps, log-levels, pid, actual message, etc.). Finally, Logstash will send the data to Elasticsearch.

We will not have to change any configurations having to do with Elasticsearch; it will simply store the data Logstash sends to it.

Finally, we will use Kibana to access the Logstash-data contained in Elasticsearch.

<!--
* sen fokus på ELK stack:
    * beskriva hur logstash tar in från olika ställen, utför transformationer, skickar till olika ställen, och koppla detta till logstash.conf-filen vi kommer ändra på senare, nämn ordet 'plugins'
    * beskriva hur elasticsearch index funkar? jag vet inte detta själv
    * beskriv hur Kibana låter en "browse elasticsearch data" och "use it to craft data visualizations" eller liknande
    * borde antagligen nämna "Elastic stack" och att Beats finns. dels tycker jag det är schysst mot användaren, som kanske vill forska om egna saker, dels visar det att vi har förståelse för att det vi använder inte är "den allra senaste iterationen" (så att säga) av stacken, och dels behöver vi inte vifta bort det faktum att det finns en 'beats-plugin' i logstash-konfigurationen från docker-elk repot

^^^ Oklart hur mycket av det här som vi vill nämna redan här. Kanske sparar vi tid på att bara skriva om det när det faktiskt dyker upp i kommande steg.
-->

<!--
## Difference between ELK stack and Elastic stack

Skriv kort om historiken, hänvisa till denna länk: https://www.elastic.co/what-is/elk-stack

-->

## Moving on with the tutorial

By now, the command you executed at the top should hopefully have completed. When it has, you will see the following in the terminal:

```
Creating docker-elk_elasticsearch_1 ... done
Creating docker-elk_kibana_1        ... done
Creating docker-elk_logstash_1      ... done
```

Since it takes some time to start the services, we will take care of the configuration first. In the next step, we will start by configuring Logstash.
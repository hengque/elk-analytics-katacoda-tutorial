In this tutorial, we will look at how to use the [**ELK stack**](https://www.elastic.co/what-is/elk-stack) (also called **Elastic Stack**) to provide monitoring/analytics for software applications.

<!-- Kanske inte bör säga att den också kallas Elastic stack. Förvisso stämmer det, men egentligen bör man ju kalla ELK för ELK och Elastic stack är snarare ELKB eller så. -->

The ELK stack is an acronym for three open-source projects:
* **Elasticsearch**, an index-based search and analytics engine
* **Logstash**, a data processing pipeline that can take in data from many different sources, perform transformations on the data, and output it to several different destinations
* **Kibana**, a graphical user interface which allows the creation of many different data visualizations based on data from Elasticsearch

As the tutorial progresses, we will have more to say about each of these tools.

**NB:** The base application to monitor/provide analytics for in this tutorial will be a Java application that uses the Spring framework. However, the focus of the tutorial is *not* to cover the ins and outs of how logging is done in this particular framework; it is simply used as a template application that will generate some logs for us.

Indeed, the material in this tutorial will be applicable for whatever language and framework you use, as long as you know how to create log files in your environment of choice.

<details>
<summary>Click me!</summary>

<div style="display: block;
  margin-left: 10px;
  margin-right: 10px;
  background-color: aliceblue;
  padding: 1em;">
Throughout the tutorial, you will find expandable boxes like this one that contains extra information for the curious reader. They will also often include reference links to sites where you can learn even more about the content presented in this tutorial.

</div>

</details>

With this introduction out of the way, let's get started!
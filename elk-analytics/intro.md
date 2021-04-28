In this tutorial, we will look at how to use the [**ELK stack**](https://www.elastic.co/what-is/elk-stack) (also called **Elastic Stack**) to provide monitoring/analytics for software applications.

The ELK stack is an acronym for three open-source projects:
* **Elasticsearch**, an index-based search and analytics engine
* **Logstash**, a data processing pipeline that can take in data from many different sources, perform transformations on the data, and output it to several different destinations
* **Kibana**, a graphical user interface which allows the creation of many different data visualizations based on data from Elasticsearch

As the tutorial progresses, we will have more to say about each of these tools.

**NB:** The base application to monitor/provide analytics for in this tutorial will be a Java application that uses the Spring framework. However, the focus of the tutorial is *not* to cover the ins and outs of how logging is done in this particular framework; it is simply used as a template application that will generate some logs for us.

Indeed, the material in this tutorial will be applicable for whatever language and framework you use, as long as you know how to create log files in your environment of choice.

With this introduction out of the way, let's get started!
<p></p>

## Persisting our log messages

(**NOTE:** Make sure the base application is not running as you perform the steps below.)

To make the logs persist in a log file, we need to specify this in the settings of our application. In Java Spring, this is done in the `application.properties` file in the `src/main/resources` folder. As we do not have any settings yet, we will have to create the file as well.

Make sure you are still in the `gs-serving-web-content` folder, and execute:

`echo "logging.file.path=/root/logs" > src/main/resources/application.properties`{{execute}}

<details>
<summary>Details of application.properties</summary>

<div style="display: block;
  margin-left: 10px;
  margin-right: 10px;
  background-color: aliceblue;
  padding: 1em;">
The <code>application.properties</code> file can be used to specify various application properties (hence the name) for Java Spring applications. Many properties can also be specified directly as command line options when starting the application. Since we always want logs to persist in this tutorial, we are using the properties-file instead of command line options. </br>
(For a list of common properties, <a href="https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-application-properties.html">this</a> is a useful reference.</br>

</div>

</details>

This will make sure our logs will end up in a file in the `/root/logs` folder (the file will be automatically named `spring.log`).

<div style="display: block;
  margin-left: 10px;
  margin-right: 10px;
  background-color: #cbcbcb;
  padding: 1em;">
In this part of the tutorial, you are encouraged to research how to implement "logging to file" in your preferred language/framework, in case you want to use this tutorial with an application not written using Java Spring. Apart from specific grok-patterns for parsing our log-messages (Step 6 will explain what this means), the rest of the tutorial will be useful regardless of how the base application is implemented.
</div>

As previously stated, this tutorial is not about Java logging. Because of this, we have already added logging statements to the base application you cloned in the last step. If you are interested in how this works, take a look at any of the classes for the endpoints (you can find all endpoints in the `src/main/java/com/example/servingwebcontent` folder).

Now, with our newly added log-folder, let's again start the base application and make sure everything is working. Still in the `gs-serving-web-content` folder, start the base application:

`./mvnw spring-boot:run`{{execute}}

When it has started, you should be able to see the log messages appear in the `/root/logs/spring.log` file as well. Open a new terminal tab at this location and invoke `cat /root/logs/spring.log` to make sure the log file is being updated with your log messages.

<!--
(TODO: Kanske ha en predefined tab här, eller på ngt sätt göra detta steg lite "snällare" (något execute-kommando eller så). Kanske inte ens ber dem gå till rätt mapp i den nya tabben utan istället bara säger åt dem att köra `cat /root/logs/spring.log` i nya tabben? Tror man t om kan ha en predefined tabb som dyker upp i ett visst steg, och som kör ett visst kommando när den öppnas. Det vore ju perfekt här).
-->

Now, it is high time to download and start using the ELK stack!
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

In this part of the tutorial, you are encouraged to research how to implement "logging to file" in your preferred language/framework, in case you want to use this tutorial with an application not written using Java Spring. Apart from specific grok-patterns for parsing our log-messages (Step 6 will explain what this means), the rest of the tutorial will be useful regardless of how the base application is implemented.

Now, as previously stated, this tutorial is not about Java logging. Because of this, we have already added logging statements to the base application you cloned in the last step. However, to not make that part too "magical", let's quickly see how this is done by adding some logging statements in the `/greeting`-endpoint.

You can find all endpoints in the `src/main/java/com/example/servingwebcontent` folder. Open the `GreetingController.java` file, and change it by adding the following imports:

```
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
```

and create a `Logger` as a field in the class:

```
private static final Logger logger = LoggerFactory.getLogger(GreetingController.class);
```

and add a statement in the `greeting`-method (before the return statement) to produce a log statement with log-level `INFO` when someone is greeted:

```
logger.info("Greeted: " + name);
```

(If you are unsure if you got it right, have a look at how it is done in the `/generate-errors`-endpoint. You can find it in the `ErrorController.java` file, in the same folder as the Greeting controller.)

Now, with the newly added logging in the `/greeting`-endpoint, and especially our newly added log-folder, let's again start the base application and make sure everything is working. Still in the `gs-serving-web-content` folder, start the base application:

`./mvnw spring-boot:run`{{execute}}

When it has started, you should be able to see the new log messages we added to the `/greeting`-endpoint. More importantly, though, these messages should also appear in the `/root/logs/spring.log` file.

Open a new terminal tab at this location and invoke `cat spring.log` to make sure the log file is being updated with your log messages.

(TODO: Kanske ha en predefined tab här, eller på ngt sätt göra detta steg lite "snällare" (något execute-kommando eller så). Kanske inte ens ber dem gå till den tabben utan istället bara säger åt dem att köra `cat /root/logs/spring.log`?).

Now, it is high time to download and start using the ELK stack!
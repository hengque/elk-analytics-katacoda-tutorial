## Getting our base application up and running

First, we need a base application that will generate logs. We will use a slightly modified version of a Java Spring webpage example repo (forked from [this](https://github.com/spring-guides/gs-serving-web-content)). Let's clone this modified version:

`git clone https://github.com/andreaskth/gs-serving-web-content.git`{{execute}}

*(Tip: You can click the code box to automatically enter the command in the Katacoda terminal!)*

This modified version extends the original one by adding a few HTTP endpoints that will spawn some logging for us to use with ELK.

To start the application, go into the recently cloned repo:

`cd gs-serving-web-content`{{execute}}

and use the Maven wrapper (`mvnw`) to trigger the installation of dependencies and start the application:

`./mvnw spring-boot:run`{{execute}}

<details>
<summary>Details of command</summary>

<div style="display: block;
  margin-left: 10px;
  margin-right: 10px;
  background-color: aliceblue;">
The <code>mvnw</code> script in the command above is known as a Maven wrapper. Maven is a widely used build tool for Java (Gradle and Ant are popular alternatives), and the Maven wrapper is a script that can be used to avoid having to install Maven before using it.</br>
(You can read more about it <a href="https://www.baeldung.com/maven-wrapper">here</a> and <a href="https://stackoverflow.com/questions/38723833/what-is-the-purpose-of-mvnw-and-mvnw-cmd-files">here</a>).</br>
</br>
In the command above, we use the Maven wrapper to start the Spring Boot application by passing the <code>run</code> goal to it.

</div>

</details>

This will take roughly 15 seconds the first time, since the Maven dependencies will be pulled from a central repository (these dependencies will be cached locally to make subsequent runs faster).

More text.
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
  margin-top: 1em;
  margin-bottom: 1em;
  margin-left: 30px;
  margin-right: 30px;
  background-color: aliceblue;">
The mvnw script in the command above is known as a Maven wrapper. <b>Bold text</b> and <code>code text</code>
</div>

</details>

This will take roughly 15 seconds the first time, since the Maven dependencies will be pulled from a central repository (these dependencies will be cached locally to make subsequent runs faster).

More text.
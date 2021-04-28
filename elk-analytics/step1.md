## Getting our base application up and running

First, we need a base application that will generate logs. We will use a slightly modified version of a Java Spring webpage example repo (forked from [this](https://github.com/spring-guides/gs-serving-web-content)). Let's clone this modified version:

`git clone https://github.com/andreaskth/gs-serving-web-content.git`{{execute}}

*(Tip: You can click the code box to automatically enter the command in the Katacoda terminal!)*

This modified version extends the original one by adding a few HTTP endpoints that will spawn some logging for us to use with ELK.

To start the application, go into the recently cloned repo:

`cd gs-serving-web-content`{{execute}}

and use the Maven wrapper (`mvnw`) to trigger the installation of dependencies and start the application:

`./mvnw spring-boot:run`{{execute}}

This will take roughly 15 seconds the first time, since the Maven dependencies will be pulled from a central repository (these dependencies will be cached locally to make subsequent runs faster).

<details markdown="1">
<summary>Details of command</summary>
<hr>
<center>
<b>What did that command just do?</b></br></br>
</center>

```
Another test to see which looks best on Katacoda. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
```
<hr>

</details>

<br/>
More text.
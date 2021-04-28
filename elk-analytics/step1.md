## Getting our base application up and running

First, we need a base application that will generate logs. We will use a slightly modified version of a Java Spring webpage example repo (forked from [this](https://github.com/spring-guides/gs-serving-web-content)). Let's clone this modified version:

`git clone https://github.com/andreaskth/gs-serving-web-content.git`{{execute}}

*(Tip: You can click the code box to automatically enter the command in the Katacoda terminal!)*

This modified version extends the original one by adding a few HTTP endpoints that will spawn some logging for us to use with ELK.

## Persisting our log messages

Se till att applikationen är avstängd.

Oklart om vi bara vill säga "klicka här" (och isf förtydliga att de måste vara kvar i 'gs-serving-web-content'-mappen):
`echo "logging.file.path=/root/logs" > src/main/resources/application.properties`{{execute}}

Eller om man ska be dem navigera editorn och lägga till den manuellt. Hmm, när jag testade detta själv nu dock (att navigera i editorn dvs) var det riktigt onice. Dels är scroll-delen rätt dålig på så sätt att man inte riktigt kan scrolla längst ner (jag måste klicka på 'expand all'-knappen längst upp och sen scrolla igenom allt för att hitta rätt) och sen var det ganska o-ergonomiskt att lägga till en ny fil. Man högerklickade och valde new, och när den var skapad så collapse:ade allt i hierarkin igen så man var tvungen att hitta den igen... Så jag tror jag föredrar det övre sättet.

(Okej, vi skulle kunna använda Katacodas open-syntax kanske! https://www.katacoda.community/scenario-syntax.html#open) Testar:

`src/main/resources/application.properties`{{open}}
`/root/gs-serving-web-content/src/main/resources/application.properties`{{open}}

**EDIT:** Efter att ha testat denna 'open'-syntax så verkar den inte funka... Inte för mig iaf.

Iaf, så förklarar vi snabbt att i Java Spring sköts applikations-inställningar i denna fil (och länkar till en eller två referenser där de kan läsa mer om de vill veta mer). Kan även lägga in något stycke här som säger att "i den här delen av tutorial:en kan du nu välja att hitta information på internet om hur man gör detta i den miljö du vill använda, ty resten av tutorial:en kommer gå rätt bra att följa ändå" (några grejer är fortfarande lite Java-baserade dock, framför allt våra grok-patterns som gör antaganden om hur logg-meddelanden ser ut).

Sen säger vi något i stil med "As previously stated, this tutorial is not about Java logging. Because of this, we have already added logging statements to the base application you cloned in the last step. However, to not make that part too 'magical', let's quickly see how this is done by adding some logging statements in the `/greeting`-endpoint" eller så.

Ber dem öppna GreetingController (här vore det också nice med Katacoda-open), importera loggers, skapa fältet, lägga till logger.info-statement i get-metoden.

"Now, with the newly added logging in the /greeting-endpoint, and especially our newly added log-folder, let's again start the application and make sure everything is working. Still in the gs-serving-web-content folder, start the base application:

`./mvnw spring-boot:run`{{execute}}
"

Sen något sista stycke här om att de bör kunna gå till 'logs'-mappen (antingen beskriver vi hur de öppnar en ny terminalflik med +, eller så har vi redan en predefined tab för det) och köra 'cat' på spring.log, och att deras greetings-log också borde dyka upp om de gjort rätt.

(Antagligen specificerar vi också hur deras greetings-loggmeddelanden bör se ut, så vi kan hjälpa dem med grok-patterns i ett senare steg).

"Now, it is high time to download and start using the ELK stack"
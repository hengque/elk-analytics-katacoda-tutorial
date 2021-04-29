## Introducing: The ELK stack

"First of all, it will take some time to fetch and build the images needed to get the stack up and running. Therefore, it's suggested that you clone the stack and invoke docker-compose right now, and then read the information about ELK as the stack is setting up:"
(påpeka att det kan ta 2-3 minuter, och att det främst beror på den VM som denna instans av tutorial:en kör på)

(se till att man är tillbaka i /root, kanske genom att ha detta i en ny terminal)

`git clone https://github.com/deviantony/docker-elk.git`{{execute}}

`cd docker-elk`{{execute}}

`docker-compose up --no-start`{{execute}}

(lägg in en aside om vad docker-compose gör, och framför allt att --no-start gör att den hämtar allt den behöver och bygger images, men startar inte. detta för att vi vill ändra lite i konfigurationen innan vi startar)

Förklara också att det finns olika sätt att köra ELK på; man måste ju inte köra containerized men vi gör det för enkelhetens skull ("the docker-elk repo allows for quick setup of the stack so we can focus on actually using it", typ). Kan även använda "hosted version" (länk till det) och även installera komponenterna var för sig.

Skriv lite info här om:
* kort om "varför log management?" (nämn stora applikationer med sjukt många meddelanden, vill kunna aggregera dem på bra sätt; nämn distribuerade applikationer (främst microservices) där en stor del av det är att samla in dem från olika källor)
* kort (bara en mening) nämna andra verktyg som finns? (Nagios, Splunk tror jag är två)
* sen fokus på ELK stack:
    * beskriva hur logstash tar in från olika ställen, utför transformationer, skickar till olika ställen, och koppla detta till logstash.conf-filen vi kommer ändra på senare, nämn ordet 'plugins'
    * beskriva hur elasticsearch index funkar? jag vet inte detta själv
    * beskriv hur Kibana låter en "browse elasticsearch data" och "use it to craft data visualizations" eller liknande
    * borde antagligen nämna "Elastic stack" och att Beats finns. dels tycker jag det är schysst mot användaren, som kanske vill forska om egna saker, dels visar det att vi har förståelse för att det vi använder inte är "den allra senaste iterationen" (så att säga) av stacken, och dels behöver vi inte vifta bort det faktum att det finns en 'beats-plugin' i logstash-konfigurationen från docker-elk repot

Efter att användaren läst detta borde Katacoda (förhoppningsvis) ha hämtat allt och byggt images. (eller 'byggt containers' eller vad initialiseringen nu kallas. får kolla upp det så vi skriver rätt)

Om den inte har det är det antagligen okej att gå vidare till nästa steg och börja läsa om logstash dock. Hursomhelst vill vi någonstans säga att när det står

```
Creating docker-elk_elasticsearch_1 ... done
Creating docker-elk_kibana_1        ... done
Creating docker-elk_logstash_1      ... done
```

så är den klar.

Eftersom att ingen data kommer finnas där ännu så tycker jag det bästa är att konfigurera saker i nästkommande steg innan vi drar igång stack:en.

Så vi skriver någon övergångsmening om att vi nu ska konfigurera stack:en så att logstash hämtar data från vår fil och skickar till ES, och kibana hämtar data från ES:s logstash-index. Och så hänvisar till nästa steg (steg 4).
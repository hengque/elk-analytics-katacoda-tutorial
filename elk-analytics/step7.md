<p></p>

## Creating data visualizations with Kibana Dashboard

Once again, navigate to the hamburger menu and this time click on `Dashboard`, just below `Discover`. Click `Create a new dashboard`, then `Create panel`, and choose `Lens`. You can now drag one of the fields from the left into the middle area and a graph will automatically be created for that field.

The default suggestions of Kibana when you try this with different fields will often not be what you want, however. So, we will now showcase three different ways you can visualize data.

## Ratio of info to error message

Välj donut-chart.
Dra in log_level.keyword.
För finare färger, gå till panelen till höger och klicka på vad det nu står där, scrolla ner till color palette, och välj "Status"

Såhär ser det ut när den är skapad (@Henrik: mitt förslag är att vi inte inkluderar bilder varje steg här, utan bara en fin bild i slutet på hur de tre ser ut tillsammans; bilderna här är bara för "debugging" för oss):

![Errors-before](./assets/errors-before.png)

Och sen anropar vi `/generate-errors`-endpointen:

![Errors-generated](./assets/errors-generated.png)

Och klickar sedan på Refresh i dashboarden för att se:

![Errors-after](./assets/errors-after.png)

<hr>

## Show who's popular (i.e. most greeted)

Välj data table.
Dra in greeted.keyword
Borde räcka

![Names-before](./assets/names-before.png)

Och sen anropar vi `/greeting`-endpointen några ggr och klickar sedan på Refresh i dashboarden för att se:

![Names-after](./assets/names-after.png)

## How are people using the calculator?

TODO Henrik.

## Final result

Lägg in fin bild på vår Dashboard.
<p></p>

## Creating data visualizations with Kibana Dashboard

Once again, navigate to the hamburger menu and this time click on `Dashboard`, just below `Discover`. Click `Create a new dashboard`, then `Create panel`, and choose `Lens`. You can now drag one of the fields from the left into the middle area and a graph will automatically be created for that field.

The default suggestions of Kibana when you try this with different fields will not always be exactly what you want, however (if you dragged some random fields to the middle area, you can always reset it by clicking the red `Reset layer` button to the right). So, we will now showcase three different ways you can visualize data. The first two are relatively simple, and the third one is a bit more involved.

(Remember to save the graphs by clicking `Save and return` in the top right when you are done with them)

## Ratio of info to error messages

Pick the `Donut` chart-type from the dropdown. From the left area, drag the `log_level.keyword` field to the middle area. To change the colors to be more indicative, go to the area on the right and click `Top values of log_level.keyword`, scroll down to `Color palette`, and pick *Status* instead of *Default*.

This is what the resulting graph could look like:

![Errors-before](./assets/errors-before.png)

If you invoke the `/generate-errors`-endpoint in the base application and hit `Refresh`, the graph will change:

![Errors-after](./assets/errors-after.png)

(When you are done, don't forget to save the graph by clicking `Save and return` in the top right!)

<hr>

## Show who's popular (i.e. most greeted)

Pick the 'Data table' chart-type from the dropdown. From the left area, drag the `greeted.keyword` field to the middle area.

This is what the resulting graph could look like:

![Names-before](./assets/bunny-data-table.png)

## How are people using the calculator?

The calculator has been prepared with multiple logging utilities to allow various visualizations to be made. The following is logged:
- if the calculator is accessed through a GET request (i.e. it is opened through the calculator-endpoint) or a POST request (i.e. the page is reloaded after doing a calculation)
- if the provided expression is valid, invalid, or a division with 0 (which although invalid is separated into its own case)
- assuming the expression is valid, the number of times each operator was encountered in the expression
- and lastly what the numeric value of the result was (given a valid expression)

Feel free to come up with various ways to visualize these results graphically in Kibana. Here, we shall just showcase a few simple examples.

<b style="font-size:20px;">1. A graph showing the distribution between valid, invalid and zero-division expressions</b>  

Open a new panel of type `Lens`. Drag and drop `calc_expr_validity.keyword` from the left area to the middle area. You should now have a suggested graph for this field. 

To get the graph shown in the below image, choose the graph type `Pie` in the dropdown just above the graph. If you want to change the color palette, click the box under `Slice by` in the area to the right of the graph. Here you have several options, one of which is "Color palette".

You should now have a graph that looks something like this:
![Calculator-expression-validity](./assets/calc_validity_graph.png)

(Make sure to invoke the `/calculator` endpoint in the base application with some invalid expressions such as divisions by zero or things like `7 + *` to make the graph more interesting!)

<b style="font-size:20px;">2. A graph showing how many times operators appear in expressions</b>

Open a new panel of type `Lens`. Start by creating 3 additional layers; this can be done by clicking the plus symbol at the bottom of the right area. This is necessary to allow multiple fields to be added to a single graph. Next drag and drop `calc_additions.keyword`, `calc_divisions.keyword`, `calc_multiplications.keyword` and `calc_subtractions.keyword` from the left area to the middle area. You should now have a suggested graph for these 4 fields. 

To get the graph shown in the image below, choose the graph type `Bar` in the dropdown just above the graph. Note: some graph types are not available when having multiple layers; if you choose one of those types (indicated by a warning sign in the dropdown) it will remove some of your layers.

Click the "bar symbols" above the graph to rename the axis.
Next, in the layers to the right click the box under `Vertical axis` to rename the data series. Do this for all 4 layers and then click `Save and return` at the top right of the Kibana interface. 

You should now have a graph that looks something like this:
![Calculator-operators](./assets/calc_operator_graph.png)

This graph shows that the vast majority of the valid expressions come from users entering a number without any operators (and also pressing the equals button to evaluate it). This is the leftmost group of bars. Each bar represent how many expression have been evaluated without the corresponding operator (for instance the purple bar shows that 12 expressions have been evaluated without any subtractions). Note that an expression such as `5+6-2` would increase the bars of multiplications and divisions by 1 since they are missing.

The middle group shows how often an operator has appeared exactly once in an expression (`3+2-5-3` has `+` exactly once, `24/8` has `/` exactly once, and so on). For instance, the middle blue bar shows that only two expressions containing exactly one division have been evaluated. Lastly, the third group shows that the only operator that has appeared more than once in an expression is the multiplication operator, appearing twice in one expression (for example: `5*3 + 8*9`).

<b style="font-size:20px;">3. A graph showing how the traffic of the calculator page varies over time</b>  

Open a new panel of type `Lens`. Drag and drop `calc_request.keyword` from the left area to the middle area. You should now have a suggested graph for this field. In the area to the right of the graph, click the box under `Horizontal axis` (it probably says "Top values of calc_request.???keyword"). 

Next choose `Date histogram` at the top. This should automatically give you a time graph for the time period specified previously. If you chose some high value here (that was way above the time you have spent with this tutorial) you might have a rather boring graph with just a bar or two to the far right. 

If you manage to keep the tutorial going for long enough and keep using the calculator, this will become more interesting. But perhaps more interesting for the time being would be to adjust the timeframe to the one you have spent in the tutorial. Like before this can be done to the right of the search bar (remember to click apply). But you can also click and drag over the area of the graph that you want to "zoom in" on to automatically tighten your timeframe. Doing this a couple of times might give you a graph looking something like the one below. Do note that this timeframe will affect how you view data in the rest of Kibana as well. So in case some of your data appears to be missing you might have to widen your timeframe.

Worth noting is that Kibana automatically chooses the width of the bars for you (for instance it might make it so that each bar covers 30 seconds in time). You can manually change this in the same menu you chose `Date histogram` earlier.

![Calculator-traffic](./assets/calc_traffic_graph.png)


## Final result

If you have followed along with all the graphs we have created your `Dashboard` might look something like this (with some manual resizing of the graphs):

![Dashboard](./assets/dashboard.png)

(Remember to save the dashboard before browsing to something else in Kibana)

# Breakout 3 - Logs

#### Explore

Jump to explore mode and select Loki-TNS as the data source
In the query builder, first make sure ```builder``` is selected.
Lets select Job as our label and tns_app. Run query 
Review some of the output logs! Unfold a few that look interesting. 



<img width="1279" alt="Screenshot 2023-06-15 at 12 41 09 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/1de75d22-e263-46b2-83f7-d2f09a1ed4a0">

Add an operation such as a line filter that contains “error”

<img width="1279" alt="Screenshot 2023-06-15 at 12 42 39 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/1f731e3d-33f7-4767-9eea-ce3e0af2c033">

Great! Using the query builder you've done some basic log querying and grepping. 

While a logs volume graph exists, lets add a few more operations in explore. The end result is something you could use in a dashboard.

In our query builder add another operation:
The first will be a counter over time operation, you can start typing counter and it will auto fill. Last operation to add is sum by label

You should see a graph output,taking your query summing the job and counting over time specifically any log lines with error
<img width="1279" alt="Screenshot 2023-06-15 at 12 46 34 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/b3c48481-610c-4c63-b6bb-651dd6ff9645">

_____

#### Dashboard annotations

Let's go back to our original Intro workshop dashboard. Feel free to navtigate via main menu or leverage command palette.
In the top right there is a settings gear, this settings gear is for the dashboard that allows you to edit general dashboard properties such as time settings, dashboard variables, add links, view the raw json and more. 

<img width="1297" alt="Screenshot 2023-06-15 at 12 49 35 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/6c0090d8-8697-4478-bae2-f58c28f08f00">

Once we are in the settings we want to visit the annotation section 
<img width="383" alt="Screenshot 2023-06-15 at 12 50 01 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/a797d154-633f-49f2-88cd-4637412e4119">


Click Add Annotation query

- Name Loki Error
- Data source = Loki-TNS
- Show in selected panels: Client QPS

- Query box insert: 

```{job="tns_app"} |= "error"```
- Apply and click close in the top right to go back to the dashboard

<img width="1116" alt="Screenshot 2023-06-15 at 12 52 14 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/84daf1b8-8f8e-48d3-bf91-87bf1b7b2b22">

_____

On the top youll have a button that can enable or disable the annotations we just added. 

<img width="1024" alt="Screenshot 2023-06-15 at 12 53 38 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/4394ae06-1a68-45a2-9350-8831084461c0">

Ensure its enabled and in the client QPS panel you should see a line indicating there is an annotation. 

Hover over the annotation line:

Annotations provide a way to mark points on the graph with rich events. When you hover over an annotation you can get event description and event tags. The text field can include links to other systems with more detail. in our example we are looking at a specific log stream, grepping for anything with error.
![Kapture 2023-06-15 at 12 54 43](https://github.com/nikoalch/intro-grafana/assets/33036213/a2d2db13-8e33-4c4f-9924-796104f16936)

_____

##### Add another visualization for logs

Add a new visualization panel in the dashboard, 
- Select logs as the visualization 
- Select: Loki-TNS as the data source
- Select: ```job=tns_app``` as filter
- Give the Panel title an appropriate name such as TNS App logs. 

*Note: Naming panels is incredibly important to help give end users context, especially those who may not be familiar with the dashboard/services/etc.* 

<img width="1278" alt="Screenshot 2023-06-15 at 12 58 10 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/ba82f9ff-03cd-4524-8d10-5eb3b0c94c4e">

Drag to the bottom and resize logs panel at the bottom of the dashboard to fit

_____

#### Bonus: Metrics to Logs correlation

- in the App row, go to the QPS panel.
- select time range of interesting event
- from the panel menu -> go to explore 
- from explore split the pane
- change data source to loki
- 🎉 just completed metrics to logs correlation for a specific metric to the related log service 


![Kapture 2023-06-15 at 13 02 24](https://github.com/nikoalch/intro-grafana/assets/33036213/eb39f0dd-afd1-4990-ae7e-3dac82bee230)


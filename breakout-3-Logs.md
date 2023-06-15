# Breakout 3 - Logs

#### Explore

Jump to explore mode and select Loki-TNS as the data source
In the query builder, first make sure ```builder``` is selected.
Lets select Job as our label and tns_app. Run query 
Review some of the output logs! Unfold a few that look interesting. 


<img width="1279" alt="Screenshot 2023-06-15 at 12 41 09 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/26f48e22-2e44-493e-a78b-ccf6bd25e845">

Add an operation such as a line filter that contains “error”
<img width="1279" alt="Screenshot 2023-06-15 at 12 42 39 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/63f59985-1ee8-476f-988b-b382a9858eb3">

Great! Using the query builder you've done some basic log querying and grepping. 

While a logs volume graph exists, lets add a few more operations in explore. The end result is something you could use in a dashboard.

In our query builder add another operation:
The first will be a counter over time operation, you can start typing counter and it will auto fill. Last operation to add is sum by label

You should see a graph output,taking your query summing the job and counting over time specifically any log lines with error
<img width="1279" alt="Screenshot 2023-06-15 at 12 46 34 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/f484f541-f058-4d87-b076-9db2877cf2a3">

_____

#### Dashboard annotations

Let's go back to our original Intro workshop dashboard. Feel free to navtigate via main menu or leverage command palette.
In the top right there is a settings gear, this settings gear is for the dashboard that allows you to edit general dashboard properties such as time settings, dashboard variables, add links, view the raw json and more. 
<img width="1297" alt="Screenshot 2023-06-15 at 12 49 35 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/5f3b401e-7c70-4455-b840-03ea0b1bc656">

Once we are in the settings we want to visit the annotation section 
<img width="383" alt="Screenshot 2023-06-15 at 12 50 01 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/988ebf8c-d855-4f61-86cc-e62fb1854372">

Click Add Annotation query

- Name Loki Error
- Data source = Loki-TNS
- Show in selected panels: Client QPS

- Query box insert: 

```{job="tns_app"} |= "error"```
- Apply and click close in the top right to go back to the dashboard
<img width="1116" alt="Screenshot 2023-06-15 at 12 52 14 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/4985842a-d367-4821-873b-1aa1690f77ad">

_____

On the top youll have a button that can enable or disable the annotations we just added. 
<img width="1024" alt="Screenshot 2023-06-15 at 12 53 38 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/f7e555c7-ec9c-425f-b3b2-3a40fe78c6e6">

Ensure its enabled and in the client QPS panel you should see a line indicating there is an annotation. 

Hover over the annotation line, what do you see?
![Kapture 2023-06-15 at 12 54 43](https://github.com/nikoalch/intro-grafana/assets/33036213/7dc9e1e6-f173-48a7-8172-570275b60062)


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

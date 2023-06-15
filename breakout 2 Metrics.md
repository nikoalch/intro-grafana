# Breakout 2 - Metrics

#### Explore and querying
Visit the explore page where we will be running through a few PromQL query examples. 
<img width="1285" alt="Screenshot 2023-06-15 at 11 40 08 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/a0c04234-6ee3-4a26-83a5-a48319dd1373">

For the below we will be using the code query editor. 
Select the ```Prometheus-TNS``` as your data source.

Switch to “code” mode in the query editor. You can leverage the builder, however it will be easier to copy/paste queries. 
<img width="218" alt="Screenshot 2023-06-15 at 11 42 04 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/20e63b7b-6bb2-4585-aa93-27ffb9abb89c">

The first query we will insert is a simple one:
```up```
Run query or hit ```shift-enter``` on your keyboard.
The up metric is probably the most popular query to run. It gives you a value of 1 (up) or 0 (down) and lets you know which jobs are running

<img width="1290" alt="Screenshot 2023-06-15 at 11 44 43 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/71f1b504-5189-4d4f-9f07-82cb254c695a">

Breaking down the metric.

```up``` = metric name
Inside the curl braces ```{ }``` are key/value labels 
In this case there are two active series for the up metric. 

If you type this query in:
```up{instance="app:80", job="tns_app"}```

In this query, we are filtering the time series further by appending labels in the curly braces. 
We are leveraging the ```=``` label selector, which will select labels that are exactly equal to the provided string.
```!=``` and ```=~``` and ```!~``` are also available for not equal to, or regex/not regex matching.
<img width="1290" alt="Screenshot 2023-06-15 at 11 59 19 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/6f6d5a48-596b-4ce0-ad2a-e0a13db96c90">

For the rest of the workshop we will primarily be working with metrics that start with “tns”
Go ahead and start typing “tns”. The query editor will start auto-populating the results

<img width="1290" alt="Screenshot 2023-06-15 at 12 00 08 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/037c9341-f2ad-497d-bfb3-f0a3c128b733">

____

#### Importing our first dashboard
Go to Dashboards Menu, New -> Import
<img width="1290" alt="Screenshot 2023-06-15 at 12 01 18 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/12798d8c-dad1-4810-90d1-467d601eda5d">

There are three ways in the UI to import a dashboard, via a json file, a ID, or pasting json. 

In this example we will want to use the import via grafana.com. 
```grafana.com/dashboards``` is a public repository of community and grafana dashboards. 
Insert the ID: ```18869``` and click “Load”
<img width="1290" alt="Screenshot 2023-06-15 at 12 02 43 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/9440a379-820e-491e-9ce7-cb7f31846ace">

Validate name, folder, and for Data source confirm “Prometheus-TNS” is selected as the datasource. 
<img width="1290" alt="Screenshot 2023-06-15 at 12 08 38 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/94613eeb-5613-4e6e-b8e5-24f52299e10a">


#### Exploring dashboard
Once the dashboard has been successfully imported. You'll see four total panels with two rows. We haven't gone over rows, but try folding and unfolding to get a gist. 

Feel free to edit any of the panels and settings, such as opacity visuals, lines, dots etc. spend a few minutes making changes and reviewing outcomes. 
<img width="1290" alt="Screenshot 2023-06-15 at 12 10 56 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/a1c20390-6446-49b3-bfe4-67e7549739f9">

To edit a panel: click the top right of a panel to show three vertical dots. 
<img width="1290" alt="Screenshot 2023-06-15 at 12 11 52 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/2d5b0918-af45-4105-8101-b07af52661a2">

#### Completing the RED dashboard
RED method of dashboards consist of:
- Rate (the number of requests per second)
- Errors (the number of those requests that are failing)
- Duration (the amount of time those requests take)
We have load balancer and app level rows. For this next exercise we will add another row and call it client. 

Click add - Row
<img width="1290" alt="Screenshot 2023-06-15 at 12 13 33 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/9e30d036-b7fc-40c7-8452-745dd27a9560">

On settings gear and rename it to “client”
Repeat for - leave blank
click Update
<img width="551" alt="Screenshot 2023-06-15 at 12 15 19 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/edcf4094-cf85-4fe1-a76d-b29c7942d64e">

Fold the row, and to the right drag the row down to the bottom. 
<img width="1290" alt="Screenshot 2023-06-15 at 12 14 22 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/2ab487ac-7d9c-493c-a451-7339cdd35314">
_____

#### Add a new Visualization / panel 
Go to the top nav bar, Click Add - > Visualization.

Ensure data source is ```Prometheus-TNS``` 
Insert query:
```sum by (status_code) (rate(tns_client_request_duration_seconds_count{job="tns_app"}[1m]))```

Unfold options in A query
Insert ```{{status_code}}``` in legend


<img width="1300" alt="Screenshot 2023-06-15 at 12 18 10 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/cf450d5c-ba2b-456a-b8ea-f3861d7c700e">

In the panel options we will change the title to “Client QPS”
In Graph Styles Section:
Line width: 0
Fill opacity: 100
Show Points: never

*Note: feel free to play around with graph styles to get a feel for output.*

Click apply on the top right

<img width="398" alt="Screenshot 2023-06-15 at 12 20 30 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/4497ebb1-2519-4cd7-b1e8-bb8f600e70cf">
_____

You should see this, let's drag the new panel down below to the client row.
<img width="1037" alt="Screenshot 2023-06-15 at 12 22 51 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/762b26c1-285c-4a52-a175-a80189de2ed9">

![Kapture 2023-06-15 at 12 24 07](https://github.com/nikoalch/intro-grafana/assets/33036213/150953df-de9e-4ba6-8e0a-ae19b37515d5)



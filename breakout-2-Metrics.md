# Breakout 2 - Metrics

#### Explore and querying
Visit the explore page where we will be running through a few PromQL query examples. 
<img width="1285" alt="Screenshot 2023-06-15 at 11 40 08 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/e827a4dd-a4f0-468d-bacc-47bf55343b6c">


For the below we will be using the code query editor. 
Select the ```Prometheus-TNS``` as your data source.

Switch to “code” mode in the query editor. You can leverage the builder, however it will be easier to copy/paste queries. 

<img width="218" alt="Screenshot 2023-06-15 at 11 42 04 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/fde501bd-ebe0-4102-945a-2876f96f629a">

The first query we will insert is a simple one:
```up```
Run query or hit ```shift-enter``` on your keyboard.
The up metric is probably the most popular query to run. It gives you a value of 1 (up) or 0 (down) and lets you know which jobs are running

<img width="1290" alt="Screenshot 2023-06-15 at 11 44 43 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/e1fea595-3b9f-4eb9-9600-b896fe4ce89c">

Breaking down the metric.

```up``` = metric name
Inside the curl braces ```{ }``` are key/value labels 
In this case there are two active series for the up metric. 

If you type this query in:
```up{instance="app:80", job="tns_app"}```

In this query, we are filtering the time series further by appending labels in the curly braces. 
We are leveraging the ```=``` label selector, which will select labels that are exactly equal to the provided string.
```!=``` and ```=~``` and ```!~``` are also available for not equal to, or regex/not regex matching.

<img width="1290" alt="Screenshot 2023-06-15 at 11 59 19 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/563073d0-9671-4548-960e-09911d0605da">

For the rest of the workshop we will primarily be working with metrics that start with “tns”
Go ahead and start typing “tns”. The query editor will start auto-populating the results

<img width="1290" alt="Screenshot 2023-06-15 at 12 00 08 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/a9040749-54b6-4c1a-b439-1137eba82b3e">


____

#### Importing our first dashboard
Go to Dashboards Menu, New -> Import

<img width="1290" alt="Screenshot 2023-06-15 at 12 01 18 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/0ab233c3-d70d-4fea-8c47-3be3f7ec3aff">

There are three ways in the UI to import a dashboard, via a json file, a ID, or pasting json. 

In this example we will want to use the import via grafana.com. 
```grafana.com/dashboards``` is a public repository of community and grafana dashboards. 
Insert the ID: ```18869``` and click “Load”

<img width="1290" alt="Screenshot 2023-06-15 at 12 02 43 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/10a44293-364f-41ac-82f7-3715162bbb88">

Validate name, folder, and for Data source confirm “Prometheus-TNS” is selected as the datasource. 
<img width="1290" alt="Screenshot 2023-06-15 at 12 08 38 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/f1dab876-2730-4da8-a1f8-fef963992b42">



#### Exploring dashboard
Once the dashboard has been successfully imported. You'll see four total panels with two rows. We haven't gone over rows, but try folding and unfolding to get a gist. 

Feel free to edit any of the panels and settings, such as opacity visuals, lines, dots etc. spend a few minutes making changes and reviewing outcomes. 

<img width="1290" alt="Screenshot 2023-06-15 at 12 10 56 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/70810f7e-f2f1-41ac-ba54-68ca4d3b38ed">

To edit a panel: click the top right of a panel to show three vertical dots. 

<img width="1290" alt="Screenshot 2023-06-15 at 12 11 52 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/e33e2693-6cc7-4d43-9236-a01c9cd2f234">

#### Completing the RED dashboard
RED method of dashboards consist of:
- Rate (the number of requests per second)
- Errors (the number of those requests that are failing)
- Duration (the amount of time those requests take)
We have load balancer and app level rows. For this next exercise we will add another row and call it client. 

Click add - Row

<img width="1290" alt="Screenshot 2023-06-15 at 12 13 33 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/730e814e-3702-458f-9382-2fdc1dc2dc34">

On settings gear and rename it to “client”
Repeat for - leave blank
click Update

<img width="551" alt="Screenshot 2023-06-15 at 12 15 19 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/4784c011-6cb7-4232-b4a1-2a3df86037fc">

Fold the row, and to the right drag the row down to the bottom. 
<img width="1290" alt="Screenshot 2023-06-15 at 12 14 22 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/062afe4e-ce92-42d5-bd7e-c56898f64ca1">

_____

#### Add a new Visualization / panel 
Go to the top nav bar, Click Add - > Visualization.

Ensure data source is ```Prometheus-TNS``` 
Insert query:
```sum by (status_code) (rate(tns_client_request_duration_seconds_count{job="tns_app"}[1m]))```

Unfold options in A query
Insert ```{{status_code}}``` in legend


<img width="1300" alt="Screenshot 2023-06-15 at 12 18 10 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/c53de95c-1929-4836-b963-c2d916c2c84b">

In the panel options we will change the title to “Client QPS”
In Graph Styles Section:
Line width: 0
Fill opacity: 100
Show Points: never

*Note: feel free to play around with graph styles to get a feel for output.*

Click apply on the top right
<img width="398" alt="Screenshot 2023-06-15 at 12 20 30 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/5e41ffc3-28b0-40a2-8256-f5d2c5863490">


_____

You should see this, let's drag the new panel down below to the client row.
<img width="1037" alt="Screenshot 2023-06-15 at 12 22 51 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/68ae8196-84d7-4aa4-930c-1d2910dd1f33">


![Kapture 2023-06-15 at 12 24 07](https://github.com/nikoalch/intro-grafana/assets/33036213/b5e57230-0df6-4896-8609-13b7e3b74e8a)

_____


Next we'll add the latency for clients. 
What we'll do is duplicate the latency panel in the app row. Click the menu bar for the panel. 
Go to More -> Duplicate

<img width="1286" alt="Screenshot 2023-06-15 at 12 27 07 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/0f908ad0-2f8c-44c7-a4c6-dfd954918722">

That action will duplicate the panel and drop it down in the row. 

<img width="1286" alt="Screenshot 2023-06-15 at 12 28 06 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/52293ba0-5a81-4dce-8338-b2a1d8cd129d">

_____

Let's edit the new panel we just duplicated. 
You can click on the same panel menu and go to edit, or hover your mouse over the panel and hit the ```e``` key on your keyboard as a shortcut to jump to the panel editor.

You should now be in edit mode, showing you three different queries. 
Since we're editing a panel that we duplicated, this will help us since we will be only slightly altering the query but expecting the latency output for clients.

For each query we want to ensure they have ```tns_client______``` metrics. 
For the first query, we want to change the metric name from:
```histogram_quantile(0.95, sum(rate(tns_request_duration_seconds_bucket[$__rate_interval])) by (le))```


To:
```histogram_quantile(0.95, sum(rate(tns_client_request_duration_seconds_bucket[$__rate_interval])) by (le))```

Second query change to:
```histogram_quantile(0.95, sum(rate(tns_client_request_duration_seconds_bucket[$__rate_interval])) by (le))```

Third query change to:
```sum(rate(tns_client_request_duration_seconds_sum[$__rate_interval])) / sum(rate(tns_client_request_duration_seconds_count[$__rate_interval]))```
<img width="1279" alt="Screenshot 2023-06-15 at 12 33 29 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/ab00e2b4-a5f4-4c69-9e1b-1f68e7cd6997">


Click apply on the top right - Save dashboard.
*Note: you can add in notes to the updates you made, useful for rolling back or others tracking changes*
<img width="1279" alt="Screenshot 2023-06-15 at 12 34 02 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/5112a464-dd04-4df1-ae2e-0a63bb3f8ec2">


##### Final output:

What we've done is essentially completed a RED style dashboard, which is for these resources show the 
- Rate (requests per second)
- Errors (number of requests failing)
- Duration (the amount of time those requests take)

The RED method is a good proxy to how happy your customers will be. If you’ve got a high error rate, that’s basically going through to your users and they’re getting page load errors. If you’ve got a high duration, your website is slow. So these are really good metrics for building meaningful alerts and measuring your SLA.

Visit ```grafana.news``` to generate traffic
- Submit links
- Refresh
Cause some 500s :) 

<img width="1279" alt="Screenshot 2023-06-15 at 12 35 49 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/239bbf96-b21a-4e18-a5ea-ee5c8ee5017e">


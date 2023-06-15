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


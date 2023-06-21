# Breakout 1 - Exploring the Grafana UI

## Login
Visit your Hosted Grafana URL and sign in if you have not already
<img width="673" alt="Screenshot 2023-06-15 at 9 28 31 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/579142ce-bd2b-44bc-9522-5255a69e080d">


#### Primary Dashboard
Once you've successfully logged into Grafana, you'll see this screen. This is the default dashboard in grafana.
<img width="1306" alt="Screenshot 2023-06-15 at 9 30 17 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/7041bfbc-3357-45b2-a752-71d4826f9d9e">

*Note: this is customizable, see https://play.grafana.org/ of what an example default dashboard looks like*
_____

#### Navigate

On the top left click the home “sandwich” icon and get familiar with the menu, checking out each section.    
<img width="780" alt="Screenshot 2023-06-15 at 9 31 25 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/ff82cdbc-ce5d-4082-93df-2ed384a6e58d">


#### Command Palette 

If you’re not familiar with the command palette, it’s a feature available in many applications that allows the user to perform various actions with a few keystrokes. In code editors, programmers can use it to go to different files or perform simple tasks without taking their hands off the keyboard. 
On some websites, a command palette can be used to navigate to different areas or do other tasks that are usually performed by clicking menus or buttons. Command palettes make work more efficient for people who need or prefer to keep their hands on the keyboard
simply press  ``` cmd+k ``` in macOS or ``` ctrl+k ``` in Linux/Windows to see it for yourself!
<img width="1252" alt="Screenshot 2023-06-15 at 9 33 51 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/6585d24c-2c93-4135-8cc4-161cedd315a1">

You can type anything and jump directly to a dashboard, or a setting, explore, etc. 

_____

#### Data Sources / Connections

Our sample application, Grafana News, exposes metrics that are stored in Prometheus.

To visualize these metrics from Prometheus, you first need to add and configure the Prometheus Data Source Plugin in Grafana.

In the sidebar, hover your cursor over the Home (sandwich) icon, and then click connect data / Add a connection.

<img width="489" alt="Screenshot 2023-06-15 at 9 35 36 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/10be76c6-441b-4d70-83c1-a6c9ee2c2a16">

Click on Data sources & Add new data source on the top right


<img width="1296" alt="Screenshot 2023-06-15 at 9 37 04 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/67e673a6-e1e9-446f-8bea-ce8e5054da39">

Find prometheus and add that

<img width="1296" alt="Screenshot 2023-06-15 at 9 38 28 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/d7256be4-24d4-47ac-8453-f614302e54ae">

For the name box enter:
```Prometheus-TNS```

In the URL box, enter:
```https://prometheus.grafana.news```


<img width="1285" alt="Screenshot 2023-06-15 at 9 51 59 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/08081d0a-805d-4c59-b110-3f9b070e3a28">


Scroll down to the bottom and click save & test. You should see “Successfully queried”
<img width="1296" alt="Screenshot 2023-06-15 at 9 39 52 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/1c60e334-d2dc-46cf-a9dc-405d5cb9997e">

_____

#### Explore
Grafana’s dashboard UI is all about building dashboards for visualization. Explore strips away the dashboard and panel options so that you can focus on the query. It helps you iterate until you have a working query and then think about building a dashboard or If you just want to explore your data and do not want to create a dashboard, then Explore makes this much easier. 

From the Sandwich menu or command-palette, go to Explore

<img width="345" alt="Screenshot 2023-06-15 at 9 42 46 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/c583706c-d938-4e0e-b970-3fb197a03605">

Ensure you are on the ```prometheus-tns ``` data source.

<img width="1292" alt="Screenshot 2023-06-15 at 9 45 57 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/6136f571-9a75-4af7-aee4-12f13fca98f0">
<img width="220" alt="Screenshot 2023-06-15 at 9 46 46 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/8b60a510-1345-43e3-be33-6343093bb7f1">


*Note: there are two options available for prometheus in the query field. Builder and code, either option works and has a slightly differnt UI*


In the metric drop down find ```tns_request_duration_seconds_count```
*note: you can leverage auto fill by typing in the metric*
On the top right hit run query.


<img width="1285" alt="Screenshot 2023-06-15 at 9 50 42 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/a9c1e98d-3e2a-47f9-82ec-87519cd05495">

Great! We've added our first data source and we confirmed we can query metrics within explore. 

_____

#### Adding a Logging Data source

Repeating the steps above that you used to add the prometheus data source, add another data source with the type “Loki”
For the name:
```Loki-TNS```

For the url:
```https://loki.grafana.news```

<img width="1285" alt="Screenshot 2023-06-15 at 9 56 39 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/844f05d0-78f2-4fc8-93f4-29bc0b8d99ca">


Scroll down to the bottom and click save & test. You should see “Data source is working”

_____

#### Creating a new Dashboard
Lets navigate to dashboards and click NEW dashboard.

<img width="1285" alt="Screenshot 2023-06-15 at 11 22 10 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/19da6660-d4f3-47a0-bc28-dfbd650160d8">


Click add visulization from the main dashboard or the top nav bar. 

<img width="1285" alt="Screenshot 2023-06-15 at 11 22 54 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/b10cebdc-4437-49d4-8a08-a3487ba6d495">




In the next prompt, use the data source called ```-- Grafana --``` to the right. 
This is a built-in data source that generates sample data, which is useful when learning how to create Grafana dashboard panels.


<img width="1285" alt="Screenshot 2023-06-15 at 11 24 58 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/b7ce754e-f3ef-4685-aa06-f8049ba3abc8">


Familiarize yourself with the panel edit menu
- Notice query tab
- Data source selector
- Query A
- Add another random walk query, Query B
*Note: you might have to hit refresh to show the data points next to the time range~
- Notice right hand panel edit, 
- Try changing title, legend, axis, colors, etc.
- To change colors click on A-series
- Change visualization to another(bar chart, etc)


<img width="1285" alt="Screenshot 2023-06-15 at 11 26 51 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/7269b130-5772-44e2-9119-7fd1decdd65c">

- Top right, discard, save, apply.	
- Save the Dashboard, name it whatever youd like. 

Add another Visualization:

<img width="1285" alt="Screenshot 2023-06-15 at 11 28 32 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/913afb11-9588-44f6-9945-7462ac3b4d6c">

Once you've added another panel, add the --grafana-- mixed query, random walk. Save it.
Play around with the drag and drop via the panel title to reorder or resize as you see fit. 
- Save dashboard 

### End Hands-on 1



	

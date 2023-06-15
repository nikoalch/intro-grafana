# Breakout 1 - Exploring the Grafana UI

## Login
Visit your Hosted Grafana URL and sign in if you have not already
<img width="673" alt="Screenshot 2023-06-15 at 9 28 31 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/cf49a81b-d38f-42b1-8cbc-f2d3817b16c1">

#### Primary Dashboard
Once you've successfully logged into Grafana, you'll see this screen. This is the default dashboard in grafana.
<img width="1306" alt="Screenshot 2023-06-15 at 9 30 17 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/d77ba9d0-c573-4dd8-83a1-7ddcf361ce65">

*Note: this is customizable, see https://play.grafana.org/ of what an example default dashboard looks like*
_____

#### Navigate

On the top left click the home “sandwich” icon and get familiar with the menu, checking out each section.    
<img width="780" alt="Screenshot 2023-06-15 at 9 31 25 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/389b54c5-75c0-4dd9-baf0-53edb7a4fe35">

#### Command Palette 

If you’re not familiar with the command palette, it’s a feature available in many applications that allows the user to perform various actions with a few keystrokes. In code editors, programmers can use it to go to different files or perform simple tasks without taking their hands off the keyboard. 
On some websites, a command palette can be used to navigate to different areas or do other tasks that are usually performed by clicking menus or buttons. Command palettes make work more efficient for people who need or prefer to keep their hands on the keyboard
simply press  ``` cmd+k ``` in macOS or ``` ctrl+k ``` in Linux/Windows to see it for yourself!
<img width="1252" alt="Screenshot 2023-06-15 at 9 33 51 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/550b3a6c-8e7d-4654-892b-e1c6b3041ef0">

You can type anything and jump directly to a dashboard, or a setting, explore, etc. 

_____

#### Data Sources / Connections

Our sample application, Grafana News, exposes metrics that are stored in Prometheus.

To visualize these metrics from Prometheus, you first need to add and configure the Prometheus Data Source Plugin in Grafana.

In the sidebar, hover your cursor over the Home (sandwich) icon, and then click connect data / Add a connection.
<img width="489" alt="Screenshot 2023-06-15 at 9 35 36 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/1e04f77d-e9c8-4427-a2d8-48cbce6446bd">

Click on Data sources & Add new data source on the top right

<img width="1296" alt="Screenshot 2023-06-15 at 9 37 04 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/4ec26a74-8e7a-4b14-9249-3063e69cbe75">

Find prometheus and add that
<img width="1296" alt="Screenshot 2023-06-15 at 9 38 28 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/5068b1d1-7e45-464a-8127-8e9c7dce598f">

For the name box enter:
```Prometheus-TNS```

In the URL box, enter:
```https://prometheus.grafana.news```

<img width="1285" alt="Screenshot 2023-06-15 at 9 51 59 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/830cf038-a240-4193-9b66-275e811dca46">


Scroll down to the bottom and click save & test. You should see “Successfully queried”
<img width="1296" alt="Screenshot 2023-06-15 at 9 39 52 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/16a466a0-4000-4f66-945f-914c52b74254">

_____

#### Explore
Grafana’s dashboard UI is all about building dashboards for visualization. Explore strips away the dashboard and panel options so that you can focus on the query. It helps you iterate until you have a working query and then think about building a dashboard or If you just want to explore your data and do not want to create a dashboard, then Explore makes this much easier. 

From the Sandwich menu or command-palette, go to Explore
<img width="345" alt="Screenshot 2023-06-15 at 9 42 46 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/f432b731-85fb-4c1b-b799-73a173fd75f9">

Ensure you are on the ```prometheus-tns ``` data source.
<img width="1292" alt="Screenshot 2023-06-15 at 9 45 57 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/4cd7412e-ec08-4d59-8210-e7230f2bd731">

<img width="220" alt="Screenshot 2023-06-15 at 9 46 46 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/163b7c67-22ec-44fd-b95f-938ae780af23">
*Note: there are two options available for prometheus in the query field. Builder and code, either option works and has a slightly differnt UI*


In the metric drop down find ```tns_request_durations_seconds_count```
*note: you can leverage auto fill by typing in the metric*
On the top right hit run query.

<img width="1285" alt="Screenshot 2023-06-15 at 9 50 42 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/be4a696c-e29e-4257-97a1-39d27c401f4d">

Great! We've added our first data source and we confirmed we can query metrics within explore. 

_____

#### Adding a Logging Data source

Repeating the steps above that you used to add the a data source, add another data source with the type “Loki”
For the name:
```Loki-TNS```

For the url:
```https://loki.grafana.news```
<img width="1285" alt="Screenshot 2023-06-15 at 9 56 39 AM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/19cac8cb-e82f-45e8-9012-6b96a9b7d198">


Scroll down to the bottom and click save & test. You should see “Data source is working”



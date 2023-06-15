# Breakout 4 - Alerting

Alerts allow you to identify problems in your system moments after they occur. By quickly identifying unintended changes in your system, you can minimize disruptions to your services.

The most basic alert consists of two parts:
- A Contact Point - A Contact point defines how Grafana delivers an alert. When the conditions of an alert rule are met, Grafana notifies the contact points, or channels, configured for that alert. Some popular channels include email, webhooks, Slack notifications, and PagerDuty notifications.

- An Alert rule - An Alert rule defines one or more conditions that Grafana regularly evaluates. When these evaluations meet the rule’s criteria, the alert is triggered.

#### Creating a contact point

In the main menu(top left), click Alerts & IRM and then Alerting.
Or use the command-pallet(cmd-k,ctl-k) and type “alerting”
<img width="1061" alt="Screenshot 2023-06-15 at 1 32 32 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/4e30ec88-8f3b-4ecb-858b-d417550513de">

Go to Manage contact points


<img width="1061" alt="Screenshot 2023-06-15 at 2 41 52 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/35da6421-8a07-46a5-879a-dcf23b306c5d">

*Note: the contact point will use the email channel. Every Grafana Cloud instance comes with a default email contact point already added. Therefore, all we need to do is add a personal email to the configuration.*

*Note: ensure Grafana is selected as alert manager* 

Unfold the grafana-default-email
Click the pencil icon on the right-hand side to edit this
<img width="1072" alt="Screenshot 2023-06-15 at 2 43 03 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/9d7cd588-a021-427a-ab6d-0cc5cf09cd13">

Add an email address that you can access. This is how we will test our alert.

Click the Test button and then the Send test notification button in the popup. Now check your email. You should see an email from Grafana with a subject like ```[FIRING:1] (TestAlert Grafana)```
<img width="1072" alt="Screenshot 2023-06-15 at 3 00 58 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/8663f009-5d10-4219-a3b7-ca8dd4e4f85d">

Save contact point

_____

Now that Grafana knows how to notify us, it’s time to set up an alert rule:

In the sidebar, click Alerts & IRM and then Alerting. In the alerting page click Manage Alert Rules.
<img width="930" alt="Screenshot 2023-06-15 at 3 06 39 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/1b39374e-d597-4b02-8b6d-d7b8dec7afcd">

Click + Create alert rule
<img width="1032" alt="Screenshot 2023-06-15 at 3 07 59 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/d24fc3b4-e5e1-41e3-9fb7-488044b3e666">


A new page will appear with four distinct sections. Let’s review them one at a time. 

- Section 1, Set an alert rule name: “TNS-alert”

- Section 2: leave Grafana Managed Alert as the chosen alert type. 

- Ensure the Promethues-TNS datasource is selected.

- For the query we want to use 
```sum(rate(tns_request_duration_seconds_count[5m])) by(route)```

Click Run query. You should see some data in the table.

<img width="1032" alt="Screenshot 2023-06-15 at 3 09 51 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/291f4651-413b-456b-89a8-4eae274dadc1">


Now scroll down to the query B box. For Operation choose Classic condition in the edit box(pencil icon). 
For conditions enter the following: WHEN last() OF A IS ABOVE 0.1

<img width="387" alt="Screenshot 2023-06-15 at 3 11 31 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/7c40f2a8-f5e7-4588-80ef-88aa6d3fa131">
<img width="611" alt="Screenshot 2023-06-15 at 3 12 16 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/2dc8686d-06d2-4fed-a2af-130526ffcadd">

*Note: if you have a query C/ Threshold, delete that. We only want classic condition*


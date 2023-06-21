# Breakout 4 - Alerting

Alerts allow you to identify problems in your system moments after they occur. By quickly identifying unintended changes in your system, you can minimize disruptions to your services.

The most basic alert consists of two parts:
- A Contact Point - A Contact point defines how Grafana delivers an alert. When the conditions of an alert rule are met, Grafana notifies the contact points, or channels, configured for that alert. Some popular channels include email, webhooks, Slack notifications, and PagerDuty notifications.

- An Alert rule - An Alert rule defines one or more conditions that Grafana regularly evaluates. When these evaluations meet the rule’s criteria, the alert is triggered.

#### Creating a contact point

In the main menu(top left), click Alerts & IRM and then Alerting.
Or use the command-pallet(cmd-k,ctl-k) and type “alerting”

<img width="1061" alt="Screenshot 2023-06-15 at 1 32 32 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/a6a4651b-50ab-4013-8cf4-cd5666142931">

Go to Manage contact points



<img width="1061" alt="Screenshot 2023-06-15 at 2 41 52 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/d55ad1fb-55d9-4624-b603-b58852b12c1e">

*Note: the contact point will use the email channel. Every Grafana Cloud instance comes with a default email contact point already added. Therefore, all we need to do is add a personal email to the configuration.*

*Note: ensure Grafana is selected as alert manager* 

Unfold the grafana-default-email
Click the pencil icon on the right-hand side to edit this
<img width="1072" alt="Screenshot 2023-06-15 at 2 43 03 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/82f6564b-7f98-4d17-81a2-197753214f29">

Add an email address that you can access. This is how we will test our alert.

Click the Test button and then the Send test notification button in the popup. Now check your email. You should see an email from Grafana with a subject like ```[FIRING:1] (TestAlert Grafana)```

<img width="1072" alt="Screenshot 2023-06-15 at 3 00 58 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/bfd7f67d-46e3-4f46-afd4-1cbd8475e435">

Save contact point

_____

Now that Grafana knows how to notify us, it’s time to set up an alert rule:

In the sidebar, click Alerts & IRM and then Alerting. In the alerting page click Manage Alert Rules.

<img width="930" alt="Screenshot 2023-06-15 at 3 06 39 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/7ec2dd9a-702a-4e0f-8abf-18cf87f5b3df">

Click + Create alert rule

<img width="1032" alt="Screenshot 2023-06-15 at 3 07 59 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/e14bc17b-6ec9-4130-b838-b194b3ddda77">


A new page will appear with four distinct sections. Let’s review them one at a time. 

- Section 1, Set an alert rule name: “TNS-alert”

- Section 2: leave Grafana Managed Alert as the chosen alert type. 

- Ensure the Promethues-TNS datasource is selected.

- For the query we want to use 
```sum(rate(tns_request_duration_seconds_count[5m])) by(route)```

Click Run query. You should see some data in the table.

<img width="1032" alt="Screenshot 2023-06-15 at 3 09 51 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/c5a7f03f-5007-4476-9202-e54cd6314300">


Now scroll down to the query B box. For Operation choose Classic condition in the edit box(pencil icon). 
For conditions enter the following: WHEN last() OF A IS ABOVE 0.1
<img width="611" alt="Screenshot 2023-06-15 at 3 12 16 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/05478f8d-5cc8-45df-9438-609f24a8d473">
<img width="387" alt="Screenshot 2023-06-15 at 3 11 31 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/21b7a542-688f-4e41-b87b-f312fb0ebc14">



*Note: if you have a query C/ Threshold, delete that. We only want classic condition*

- Section 3:

Add a new folder, call it TNS **hit enter on keyboard**

In the next section is the eval group. 
input 30s as your name **hit enter on keyboard**  and change the evaluate every value from 1m to 30s. 

For the purposes of this tutorial, the evaluation interval is intentionally short. This makes it easier to test
Change the for to be “0m”  
<img width="741" alt="Screenshot 2023-06-15 at 3 15 25 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/891f0d5f-f964-4ed3-bc86-3018cc633313">


- Section 4:
Feel free to add any free form text.

Additionally, there is the ability to link a dashboard and panel, try adding the workshop dashboard the client panel in the “set dashboard and panel” box. 


<img width="948" alt="Screenshot 2023-06-15 at 3 17 04 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/2384c8b6-021a-473c-8c64-1a1172490958">

Scroll to the top and click Save rule & exit

_____

Because we only have one contact point (our email channel), the alert we setup will default to use it. 

As a system grows, admins can use the Notification Policies setting to organize and match alert rules to specific contact points and or route them to Grafana OnCall for on call management. 

**Once you receive the test alert in your email, it is recommended to delete the alert since this is a test and we have set a very low rule evaluation rate.**
<img width="1289" alt="Screenshot 2023-06-15 at 3 19 14 PM" src="https://github.com/nikoalch/intro-grafana/assets/33036213/9e190f7c-30fb-4711-a4c6-3dddfc5be1bb">



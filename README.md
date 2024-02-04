# Prometheus-and-Grafana
This project is focused on using Prometheus for monitoring on different levels and also implementing Grafana for data visualization :

- Infrastructure Level: CPU, RAM, Network etc
- Platform Level: Kubernetes components
- Application Level: 3rd-party and Own application

Requirements:
-  Ensure AWS-CLI and Helm are installed
- Configure AWS credentials on local machine with admin access (for project purpose)

Setup EKS cluster using EKSCTL command.

<img width="1413" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/4f47a740-917c-4c48-b83b-bc2210f703d8">


Connect to the cluster and add prometheus chart and install prometheus chart for kubernetes into the cluster

<img width="1155" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/4922e970-6da7-4714-afa2-9070639216c8">

<img width="1338" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/d6c66320-07a9-443f-94a1-231f4d2a9d3e">

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/de764df2-e959-48eb-a135-220f9b1e7798)

Port forward to grafana and prometheus service to connect to the U.I

<img width="841" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/62430c3e-1b3e-412f-9ef7-ce7d9a104700">


Access UI for prometheus and grafana (enter required credentials)


![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/ca5f1e18-1217-4c5c-a490-b44c58c61db2)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/027539fd-9a0a-4a6a-b9c3-68b398716ed5)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/716eefea-d370-4e40-ac39-1ea6cfeb6e60)

<img width="833" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/e8db7285-08d1-4151-8b30-009e1b55a0e9">


List below are the metrics gotten from the clusters including the nodes also


![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/5c3de341-f103-4dea-9b1e-1ef363699d50)


Below is a detailed metrics for the cluster

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/86c874e4-cbee-4926-815d-a5fe57539d94)


Deployed a microservice application

<img width="597" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/2c60515a-211d-4f87-a721-438d26e41661">


![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/0f486803-a146-4909-b8eb-a2773f662575)


We will launch a container dedicated to using the Curl command on the load balancer. This involves connecting to the applications through a script that establishes a loop, which create a high traffic 

<img width="941" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/87d2b0a9-e14b-44fe-8de0-716a87b423b6">

<img width="880" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/bf7e61b9-dd21-4e3e-a39e-53f195273513">

<img width="1211" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/7653f911-520a-48de-a9d8-7f43666f5f41">

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/7817711d-ea12-480b-aeac-79548e09440a)


The expression `rate(node_cpu_seconds_total{mode="idle"}[2m])` is a Prometheus query that calculates the per-second rate of change for the `node_cpu_seconds_total` metric with the `mode` label set to `"idle". This type of expression is what is used by grafana to display metrics needed.


![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/2fd7fccd-e99d-4361-8b17-827903805c4f)

There is need to get notified when something goes wrong, this is where alerting comes into play

- Define what we want to be notified about e.g when CPU usage is above is 50%
- Send notification i.e email/slack notification (will be implemented later)

We will set alert rules on any usecase we are interested e.g pod not starting. The prometheusrule handles the rules

<img width="723" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/c2f72139-1a3c-49b3-b9a6-11a32d786f0c">

When setting up this rules, its imperative to make use of the appropriate labels in the rules we plans on setting up, the highlighted lables below needs to be specified in our rule.

<img width="924" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/4e99ece2-7d9e-41c2-9f2a-eb4e572fff47">

We are setting two alerts respectively `down`and `HostHighCpuLoad`. The labels are included so that prometheusrule can include it in the alert that it has to monitor

<img width="1400" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/70efbca1-c34f-41be-9939-3f73efc3f681">

When you apply this rules, ensure you check prometheus log of config-reloader container to confirm a reload has triggered(which implies the rule has been added to the prometheus yaml file) by checking the time and confirm it occured after applying the rule.

<img width="1423" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/c47effa7-4a56-49a4-a251-d898ee327d32">

<img width="673" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/f8510c7c-0fc0-48c5-a265-c867401331f5">


The alerts have been updated.


![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/a92f7ed4-ef9d-4a91-9dc3-2ea979088363)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/636e8175-224a-431c-9a47-a70478730a95)

Let run cpustress container to generate CPU load and see if the alert will be triggered.

<img width="787" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/31633f51-1899-44ed-8b4f-a746dc59ee92">

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/efcacc39-bbc9-41b5-a5d1-cf4e2a183a01)

We have recently completed Kubernetes-level monitoring. Now, we are turning our attention to monitoring Redis, a third-party application within our microservices. To achieve this, we are utilizing an exporter that fetches metric data from the service and transforms the service-specific metrics into a format understandable by Prometheus. This exporter exposes the translated metrics through the `/metrics` endpoint. To ensure Prometheus is aware of this new exporter, we will deploy a ServiceMonitor, a custom Kubernetes resource designed for this purpose.

Deploy redis exporter, ensure you set servicemonitor to true and specify the redis service name in the helms value 


<img width="1163" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/19d2024e-f5db-4ab8-a3bc-eb5732d0b3ea">

<img width="620" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/23c15dde-146b-434a-bac8-36a011304bb9">

<img width="1220" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/6c2f31a2-8bdb-4eb8-9b5c-63260d01f8b6">

<img width="771" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/c37c5ef2-6580-4f51-b8f6-1d041eeb6682">

<img width="1284" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/ea5968f9-0582-4b7d-b8e1-90117cdc8809">

Redis-exporter is deployed by checking the targets under the status section and we can query different redis metrics.

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/270f5a1a-55b6-4fc8-b806-1a1eccbc51c1)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/aa024fa3-95d3-4410-b1d8-756ccaa4ca5b)

We can see the redis-exporter pod

<img width="924" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/744afb08-39c5-4af9-b3a7-3a38b6f08509">

<img width="687" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/fa0008a0-d359-40c8-a88e-33491294b10c">

We can setup a prometheusrule using ready made rules [Exporter rules](https://awesome-prometheus-alerts.grep.to/) to define the rules to specify for our exporters. For our redis application, we will be using [Redis rule](https://samber.github.io/awesome-prometheus-alerts/rules#redis), like the screenshot below.


![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/e8c136b3-dbbd-406f-8afc-ac105650e582)

Ensure you specified the appropriate labels and apply the rule

<img width="811" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/c594fc3a-7822-478a-b72d-dd1895c9918d">

<img width="606" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/613b11cc-f65f-4e10-8cd1-a79201438624">

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/5e0d9b96-c9dc-4078-9d6e-1285ab0560ec)

Let edit the redis pod replica to zero, to see if the redis-exporter will be triggered.

<img width="591" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/2cda3a29-b458-46a8-b4d2-0743ba9ce929">

<img width="961" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/9f089890-ef7b-4bc2-8a72-150ac1b6ac72">


![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/03f9f1ea-0c0b-4a4d-aac4-0598bd212fba)

Now lets try and create a dashboard for our redis application, we can make use of ready made dashboards from [Grafana](https://grafana.com/grafana/dashboards/), we will be making use on one of the numerous dashoard for [Redis]( https://grafana.com/grafana/dashboards/11835-redis-dashboard-for-prometheus-redis-exporter-helm-stable-redis-ha/)

Copy the ID number and import the dashboard in grafana using the number, ensure you select data source as prometheus.

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/44b16545-6d1a-40e2-81a1-8d964e125bf3)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/f7624cec-e8fe-4003-9ba7-2f790180a135)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/9fa07916-450d-41c4-959d-341a4d37b830)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/cc687c87-f9fd-4064-9bed-99ca124a73c0)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/48ad7bfd-4d72-4037-93b7-0c37a2bef9d4)

15895

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/599a35fb-59d3-4f68-b55f-44426b0871ad)

<img width="819" alt="image" src="https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/cfe264e1-0b20-473d-82bd-c0d6096b79db">

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/db6c81f3-bc7f-4b05-a1df-0e6b170aadcc)


![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/48058fec-cd23-4e68-9bb6-4d0581a8dd1c)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/45f153e5-ba8a-44dd-abc5-a6307ef63581)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/bf7faffd-0191-4071-905e-52d1a591e756)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/7981da35-2925-43ec-8ad6-79e0471a9056)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/ab02262a-9813-402e-aeca-0de5b9515915)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/194b02a7-c311-48ac-9616-f5b4bb59d930)

![image](https://github.com/Taiwolawal/Prometheus-and-Grafana/assets/50557587/b951a92c-0a07-4e70-842b-a024c11c95b1)

























# Prometheus

This is a **Work-In-Progress** Repo for learning how monitor your kubernetes clusters using prometheus and visualize using grafana.

Both Prometheus and Grafana have a very good documentation 

[Prometheus Docs]("https://prometheus.io/docs/introduction/overview/")

[Grafana Docs]("https://grafana.com/docs/grafana/latest/")

## Pre-Requisite

- Kubernetes Cluster minikuber or EKS
- Helm 



## It all starts with Monitoring 

Monitoring your Kubernetes cluster is essential for ensuring the health and performance of your applications and infrastructure. Here are some reasons why monitoring your Kubernetes cluster is important:

- Identify issues and troubleshoot: By monitoring your Kubernetes cluster, you can quickly identify issues such as application crashes, resource bottlenecks, and network problems. With real-time monitoring, you can troubleshoot issues before they escalate and impact your users.

- Optimize performance and capacity: Monitoring allows you to track the performance of your applications and infrastructure over time, and identify opportunities to optimize performance and capacity. By understanding usage patterns and resource consumption, you can make informed decisions about scaling your infrastructure and improving the efficiency of your applications.

- Ensure high availability: Kubernetes is designed to provide high availability for your applications, but this requires careful monitoring and management. By monitoring your cluster and setting up alerts, you can ensure that your applications remain available even in the event of failures or unexpected events.

- Security and compliance: Monitoring your Kubernetes cluster can help you identify potential security risks and ensure compliance with regulations and policies. By tracking access logs and other security-related metrics, you can quickly detect and respond to potential security threats.

<br></br>

## Using Prometheus for monitoring

Prometheus is an open-source monitoring and alerting system that helps you collect and store metrics about your software systems and infrastructure, and analyze that data to gain insights into their health and performance. It provides a powerful query language, a flexible data model, and a range of integrations with other tools and systems. With Prometheus, you can easily monitor metrics such as CPU usage, memory usage, network traffic, and application-specific metrics, and use that data to troubleshoot issues, optimize performance, and create alerts to notify you when things go wrong.

<br></br>

## Why Prometheus over other monitoring tools ?

Prometheus is a popular choice for Kubernetes monitoring for several reasons:

- Open-source: Prometheus is an open-source project that is free to use and has a large community of contributors. This means that you can benefit from ongoing development, bug fixes, and feature enhancements without paying for a commercial monitoring solution.

- Native Kubernetes support: Prometheus is designed to work seamlessly with Kubernetes, making it easy to deploy and integrate with your Kubernetes environment. It provides pre-configured Kubernetes dashboards and supports auto-discovery of Kubernetes services and pods.

- Powerful query language: Prometheus provides a powerful query language that allows you to easily retrieve and analyze metrics data. This allows you to create custom dashboards and alerts, and to troubleshoot issues more easily.

- Scalability: Prometheus is designed to be highly scalable, allowing you to monitor large and complex Kubernetes environments with ease. It supports multi-node architectures and can handle large volumes of data without significant performance degradation.

- Integrations: Prometheus integrates with a wide range of other tools and systems, including Grafana for visualization, Alertmanager for alerting, and Kubernetes API server for metadata discovery.

<br></br>

## Prometheus Architecture

<br></br>
![Alt text](https://prometheus.io/assets/architecture.png)

<br></br>

## What is Grafana ?

Grafana is a popular open-source data visualization and analytics platform that allows you to create custom dashboards and visualizations based on a variety of data sources. Grafana is often used for monitoring and analyzing metrics and logs in real-time, making it an ideal tool for monitoring systems and applications, including Kubernetes environments.

Grafana supports a wide range of data sources, including databases, time-series databases, and other data storage systems. It provides a powerful query language that allows you to retrieve and analyze data from these sources, and to create custom dashboards and alerts based on that data.

In addition to its powerful data visualization and analysis capabilities, Grafana is also highly extensible. It supports a wide range of plugins and integrations, including integrations with popular monitoring and logging tools like Prometheus, Elasticsearch, and InfluxDB.

## Step 1: Things to Know before starting

# 1. Why use helm?

Helm is a package manager for Kubernetes. Helm simplifies the installation of all components in one command. install using helm is recommended as you will not be missing any configuration steps and very efficient

# 2. What is Prometheus?

· Prometheus is an open-source monitoring tool

· Provides out-of-the-box monitoring capabilities for the Kubernetes container orchestration platform. It can monitor servers and databases as well.

· Collects and stores metrics as time-series data, recording information with a timestamp

· It is based on pull and collects metrics from targets by scraping metrics HTTP endpoints.

# 3. What is Grafana?

· Grafana is an open-source visualization and analytics software.

· It allows you to query, visualize, alert on, and explore your metrics no matter where they are stored.


# Steps

Step-1. We need to add the Helm Stable Charts for your local client. Execute the below command:
   
    * helm repo add stable https://charts.helm.sh/stable

Step2: Add Prometheus Helm repo

    * helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

Step 3: Create Prometheus namespace
 
    * kubectl create namespace prometheus

Step 4: above command is used to install kube-Prometheus-stack. The helm repo kube-stack-Prometheus comes with a Grafana deployment embedded ( as the default one )

    * helm install prometheus prometheus-community/prometheus

Step 5: To check whether Prometheus is installed or not use the below command

    * kubectl get pods -n prometheus

Step 6: To check the services file (svc) of the Prometheus

    * kubectl get svc -n prometheus
-----------------------------------------------------------------------------------------------

* Grafana will be coming along with Prometheus as the stable version
* This output is conformation that our Prometheus is installed successfully
* there is no need of installing Grafana as a separate tool it comes along with Prometheus

let’s expose Prometheus and Grafan to the external world
there are 2 ways to expose

1) through Node Port
2) through LoadBalancer

* let’s go with the LoadBalancer to attach the load balancer we need to change from ClusterIP to LoadBalancer
command to get the svc file.

   * kubectl edit svc stable-kube-prometheus-sta-prometheus -n prometheus

* change it from Cluster IP to LoadBalancer after changing make sure you save the file

* we can use a Prometheus UI for monitoring the EKSbut the UI of Prometheus is not a convent for the user Grafana will extract the matrix from the Prometheus UI and show it in a user-friendly manner

-----------------------------------------------------------------------------------------------------------

# let’s change the SVC file of the Grafana and expose it to the outer world

* command to edit the SVC file of grafana

    * kubectl edit svc stable-grafana -n prometheus

* use the below command to get the password

    * kubectl get secret --namespace prometheus stable-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

* the username is "admin"

# Note: we can deploy the Grafana and Prometheus with a different method:-

1. Create all configuration files of both Prometheus and Grafana and execute them in the right order.

2. Prometheus Operator — to simplify and automate the configuration and management of the Prometheus monitoring stack running on a Kubernetes cluster

3. Helm chart — Using helm to install Prometheus Operator including Grafana


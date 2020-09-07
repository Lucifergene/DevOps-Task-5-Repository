
### DevOps/Monitoring

# Deploying Prometheus and Grafana on top of Kubernetes

### Integrating monitoring tools in the Development Pipelines

![](https://cdn-images-1.medium.com/max/2590/1*2yW38UXgAuzfx8Ss2YA1wg.png)

**After a month of working with Docker, Kubernetes, GitHub and Jenkins, to create development pipelines, now is its the time to integrate monitoring tools into the existing pipelines, so that we can even automate the monitoring actions on the cloud.**

For performing the monitoring actions, we have 2 very efficient tools which work hand-in-hand, **Prometheus **and **Grafana**. In this article, we are going to implement these tools on top of Kubernetes.

### The integration would be done in the following manner:

 1. Deploying them as pods on top of Kubernetes by creating resources Deployment, Replica Set, Pods or Services.

 2. Making their data to remain persistent.

 3. Exposing both to the outside world

## Introduction

*First, let’s understand the working of the monitoring tools we are using:*

### Prometheus

**Prometheus** is an open-source system monitoring and alerting toolkit originally built at SoundCloud. Since its inception in 2012, many companies and organizations have adopted Prometheus, and the project has a very active developer and user community. It is now a standalone open source project and maintained independently of any company.

### Grafana

**Grafana** is an open-source, general-purpose dashboard and graph composer, which runs as a web application. Grafana allows you to query, visualize, alert on and understand your metrics no matter where they are stored. Create, explore, and share dashboards with your team and foster a data-driven culture.

## Assumptions

First of all, we are assuming that **Kubectl and** **Minikube **are installed in the system.

## 1. Setting up the PVC for Prometheus

Prometheus by default has ephemeral storage. Therefore we need to use a Persistent Volume Storage so that data stored does not get lost in the running pod fails. For that, we are using the **Kubernetes Persistent Volume Claim (PVC)**

To set up we need to create the following YAML file.

 <iframe src="https://medium.com/media/88848e9277ec7304ae055d62e77c4685" frameborder=0></iframe>

## 2. Deploying Prometheus Docker Image

After setting up the PVC, we now have to install Prometheus. For that first, we need to create a service to export the Prometheus using NodePort. After that, we can use the Prometheus Docker Image on Dockerhub to install the tool in Minikube.

The final YAML file would look like this:

 <iframe src="https://medium.com/media/6b8cf5491b70c5a6f4976a43b5b41e61" frameborder=0></iframe>

## 3. Setting up the PVC for Grafana

*(Same codes with minor changes)*

 <iframe src="https://medium.com/media/eaa6f149e611ef8265d5eed3f9f42f29" frameborder=0></iframe>

## 4. Deploying Grafana Docker Image

*(Same codes with minor changes)*

 <iframe src="https://medium.com/media/abc2670298375cad59c7f634f39900c0" frameborder=0></iframe>

## 5. Creating the Kustomization file

In this file, we will be mentioning the sequence in which all the files need to be created. After running this file, it will do everything, Prometheus and Grafana will have been deployed on Kubernetes and have been connected to PVC for no data loss. Both of the pods will be exposed to the outside world. Using Kubernetes, we don’t need to worry about crashes, because that is the biggest advantage of using Kubernetes, and as we are using PVC, so there will be no data loss whatsoever.

 <iframe src="https://medium.com/media/4a3b0f52c7bb2d661ba6444e3a26aaa9" frameborder=0></iframe>

To run the entire infrastructure we created, just the kustomization file has to be run with the following command:

    kubectl apply -k .

## 6. Exposing both to the outside world

We need to open the Prometheus & Grafana in the browser using the Minikube IP to get access to the monitoring tools.

![Prometheus Landing Page](https://cdn-images-1.medium.com/max/2732/1*xk9bnjAWwcgWBlgQC-MVkw.png)

![Grafana Landing Page](https://cdn-images-1.medium.com/max/2000/1*7xjq8Nplhur7pJE-P4oXyQ.png)

**And we reached the end of the solution!!!**

You can visit the repository from below:
[**Lucifergene/DevOps-Task-5-Repository**
*All codes and snippets related to Task 5. Contribute to Lucifergene/DevOps-Task-5-Repository development by creating an…*github.com](https://github.com/Lucifergene/DevOps-Task-5-Repository)

You can reach out on my [Twitter](https://twitter.com/avik6028), [Instagram](https://instagram.com/avik6028), or on [LinkedIn](https://linkedin.com/in/avik-kundu-0b837715b) if you need more help. I would be more than happy.

If you have come up to this, **do drop an 👏 if you liked this article.**

**Good Luck** 😎 and **happy coding** 👨‍💻


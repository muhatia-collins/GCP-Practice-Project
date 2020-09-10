lab: Google Cloud Fundamentals: Getting Started with GKE

 Objectives:
In this lab, you learn how to perform the following tasks:

-Provision a Kubernetes cluster using Kubernetes Engine.
-Deploy and manage Docker containers using kubectl.

Steps:

1. Confirm that needed APIs are enabled.

Use the gcloud services command to confirm that both the Kubernetes Engine API and the Containers Registry API are enabled:

gcloud services list --enabled


2. Start a Kubernetes Engine cluster.

In GCP console, on the top right toolbar, click the Open Cloud Shell button

Assign your Qwiklabs zone to an environment variable called MY_ZONE:, using the following comand:
export MY_ZONE=us-central1-a

Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:
gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

After the cluster is created, confirm your installed version of Kubernetes using the kubectl version command:
kubectl version

3. Run and deploy a container.

From your Cloud Shell prompt, launch a single instance of the nginx container.
kubectl create deploy nginx --image=nginx:1.17.10

View the pod running the nginx container:
kubectl get pods

Expose the nginx container to the Internet:
kubectl expose deployment nginx --port 80 --type LoadBalancer

View the new service:
kubectl get services

Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed

Scale up the number of pods running on your service:
kubectl scale deployment nginx --replicas 3

Confirm that Kubernetes has updated the number of pods:
kubectl get pods

Confirm that your external IP address has not changed:
kubectl get services

Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding

Congratulations!

When you have completed your lab, click End Lab. Qwiklabs removes the resources you’ve used and cleans the account for you.
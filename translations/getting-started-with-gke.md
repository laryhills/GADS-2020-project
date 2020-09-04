# LAB: Google Cloud Fundamentals: Getting Started with GKE

## Objectives

In this lab, you learn how to perform the following tasks:

    - Provision a Kubernetes cluster using Kubernetes Engine.

    - Deploy and manage Docker containers using kubectl.

## Steps:

1.  Confirm that needed APIs are enabled:

    _-_ Get a list of services that you can enable in your project:

    ```bash
        gcloud services list --available
    ```

    _-_ If you don't see the API listed, that means you haven't been granted access to enable the API.

    | API                    | SERVICE_NAME                     |
    | ---------------------- | -------------------------------- |
    | Kubernetes API         | container.googleapis.com         |
    | Container Registry API | containerregistry.googleapis.com |

    _-_ Using the applicable service name from the previous step, enable the service:

    ```bash
        gcloud services enable SERVICE_NAME
    ```

2.  Start a Kubernetes Engine cluster

    1.  For convenience, place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE:

        ```bash
            export MY_ZONE=<assigned zone>
        ```

    2.  Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:

        ```bash
            gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
        ```

    3.  After the cluster is created, check your installed version of Kubernetes using the kubectl version command:

        ```bash
            kubectl version
        ```

        _-_ The gcloud container clusters create command automatically authenticated kubectl for you.

    4.  View your running nodes:
        ```bash
            gcloud compute instances list
        ```

3.  Run and deploy a container:

    1.  Launch a single instance of the nginx container. (Nginx is a popular web server):

    ```bash
        kubectl create deploy nginx --image=nginx:1.17.10
    ```

    _-_ Note: If you see any deprecation warning about future version you can simply ignore it for now and can proceed further.

    2.  View the pod running the nginx container:

    ```bash
        kubectl get pods
    ```

    3.  Expose the nginx container to the Internet:

    ```bash
        kubectl expose deployment nginx --port 80 --type LoadBalancer
    ```

    4.  View the pod running the nginx container:

    ```bash
        kubectl get pods
    ```

    5.  Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.

    6.  Scale up the number of pods running on your service:

    ```bash
        kubectl scale deployment nginx --replicas 3
    ```

    7.  Confirm that Kubernetes has updated the number of pods:

    ```bash
        kubectl get pods
    ```

    8. Confirm that your external IP address has not changed:

    ```bash
        kubectl get services
    ```

    9.  Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.

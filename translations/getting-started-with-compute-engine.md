# LAB: Google Cloud Fundamentals: Getting Started with Compute Engine

## Objectives

In this lab, you will learn how to perform the following tasks:

    - Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

    - Create a Compute Engine virtual machine using the gcloud command-line interface.

    - Connect between the two instances.

## Steps:

1. Create a virtual machine using the Google cloud Platform (GCP) Console.

```bash
    gcloud compute instances create my-vm-1 --machine-type "n1-standard-1" --image "debian-9-stretch-v20200805" --image-project "debian-cloud" --subnet "default" --tags http

    gcloud compute firewall-rules create default-allow-http --destination=INGRESS --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http
```

2. Create a Computer Engine virtual machine using the gcloud command-line interface.

```bash
    gcloud config set compute/zone us-central1-b

    gcloud compute instances create my-vm-2 --machine-type "n1-standard-1" --image "debian-9-stretch-v20200805" --image-project "debian-cloud" --subnet "default"
```

3.  Connect between the two instances.

    1.  Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:

        _-_ Connect to my-vm-2:

        ```bash
            gcloud compute ssh my-vm-2
        ```

        _-_ ping my-vm-1 from my-vm-2:

        ```bash
            ping -c 4 my-vm-1
        ```

        _-_ Use the ssh command to open a command prompt on my-wm-1 from my-vm-2:

        ```bash
            ssh my-vm-1
        ```

        _-_ At the terminal on my-vm-1, install the Nginx web browser:

        ```bash
            sudo apt-get install nginx-light -y
        ```

        _-_ Use the nano editor to add a custom message to the homepage of the web server:

        ```bash
            sudo nano /var/www/html/index.nginx-debian.html
        ```

        _-_ Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:

        ```bash
            Hi from YOUR_NAME
        ```

        _-_ Exit the editor

            Press Ctrl+O, then press Enter to save your edited file, then press Ctrl+X to exit the nano editor

        _-_ Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:

        ```bash
            curl http://localhost/
        ```

            - Result:
                The response will be the HTML source of the web server's home page, including your line of custom text.

        _-_ To exit the command prompt on my-vm-1, execute this command:

        ```bash
            exit
        ```

        _-_ To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:

        ```bash
            curl http://my-vm-1/
        ```

    2.  Now get the external IP of the my-vm-1 instance from this command:

        ```bash
            gcloud compute instances list --zone=us-central1-a
        ```

    3.  Paste the copied IP address of my-vm-1 into a new browser tab and hit Enter:

        - Result:
          You will your web server's home page, including your line of custom text.

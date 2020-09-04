# LAB: Creating Virtual Machines

## Objectives

In this lab, you learn how to perform the following tasks:

    - Create several standard VMs.

    - Create advanced VMs.

## Steps:

1.  Create a utility virtual machine

    1. Create a VM:

    ```bash
        gcloud compute instances create utility-vm --zone "us-central1-c" --machine-type "n1-standard-1" --image "debian-9-stretch-v20200902" --image-project "debian-cloud" --subnet "default" --no-address
    ```

2.  Create a Windows virtual machine

    1. Create a VM:

    ```bash
        gcloud compute instances create windows-vm --zone "europe-west2-a" --machine-type "n1-standard-2" --image "windows-server-2016-dc-core-v20200813" --image-project "windows-cloud" --boot-disk-size "100GB" --boot-disk-type "pd-ssd" --boot-disk-device-name "windows-vm"  --subnet "default" --tags "http-server,https-server"

        gcloud compute firewall-rules create default-allow-http --direction=INGRESS --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server

        gcloud compute firewall-rules create default-allow-https --direction=INGRESS --network=default --action=ALLOW --rules=tcp:443 --source-ranges=0.0.0.0/0 --target-tags=https-server
    ```

    2. Set the password for the VM:

    ```bash
        gcloud compute reset-windows-password windows-vm
    ```

    _-_ When prompted to set or reset password, type Y

3.  Create a custom virtual machine

    1. Create a VM

    ```bash
        gcloud compute instances create custom-vm --zone "us-west1-b" --machine-type "custom-6-32768" --image "debian-9-stretch-v20200902" --image-project "debian-cloud" --subnet "default"
    ```

    2. Connect via SSH to your custom VM

       ```bash
           ssh custom-vm
       ```

       _-_ To see information about unused and used memory and swap space on your custom VM, run the following command:

       ```bash
           free
       ```

       _-_ To see details about the RAM installed on your VM, run the following command:

       ```bash
           sudo dmidecode -t 17
       ```

       _-_ To verify the number of processors, run the following command:

       ```bash
           nproc
       ```

       _-_ To see details about the CPUs installed on your VM, run the following command:

       ```bash
           lscpu
       ```

       _-_ To exit the SSH terminal, run the following command:

       ```bash
           exit
       ```

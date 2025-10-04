# Azure-Linux-Virtual-Machine-Creation-Detailed-Guide
This Repo guides you through each step using images with markups for creating a linux virtual machine in Azure portal.
and also guides you how to login to the virtual machine using ssh key from your local command prompt or git.

Additionally i will guide you through steps for creating self-host agent for using it in Azure DevOps CICD for running pipeline. 

## **Let's get started**

## **Step1: Create Virtual Machine**

Go to -> **Azure portal** -> search **virtual machine** -> open **virtual machine** -> 

<img width="1919" height="566" alt="image" src="https://github.com/user-attachments/assets/f796b694-fe87-497c-824e-7048584c43ad" />


click create -> **virtual machine** -> give **resource group** name (else click create new) -> **virtual machine** name.

<img width="1174" height="803" alt="image" src="https://github.com/user-attachments/assets/4e4c1734-0756-4f27-982a-406eca003e24" />


scroll down -> **image** choose **ubuntu server 22.04 LTS** -> **size** choose **Standard D2s_v3**

<img width="1187" height="803" alt="image" src="https://github.com/user-attachments/assets/7635ff4e-92cc-40d0-a829-39623aaf7354" />


**authentication** type choose ssh public key -> click **review + create** -> **create**.

while creating virtual machine it will show popup window click on download the ssh key, we will use this key while logging into the virtual machine.

<img width="1236" height="818" alt="image" src="https://github.com/user-attachments/assets/24aa6315-2a20-42b7-bdea-1c4df2d0bb7f" />


After creating virtual machine note down the public ip of virtual machine. it is mandatory for logging into vm.

<img width="1850" height="784" alt="image" src="https://github.com/user-attachments/assets/7338d8e8-6b8c-43d7-a670-72174213e4a2" />


## **Step2: Open the Git**

Open the Gitbash app for your laptop, go to downloads folder there you will see pem key file (prometheusvm_key.pem) which was downloaded while creating virtual machine. 

<img width="315" height="50" alt="image" src="https://github.com/user-attachments/assets/0c94ccdb-6565-4774-891f-eaa56aaebea5" />


It will look like this with you virtual machine name (prometheusvm_key.pem).

<img width="1139" height="841" alt="image" src="https://github.com/user-attachments/assets/7b0e1e1f-a9e5-44d9-86fd-713c71e5ef08" />


copy this file and paste it in ~/.ssh folder

<img width="558" height="55" alt="image" src="https://github.com/user-attachments/assets/ab79f6ca-7944-44e3-a7bd-dcef2d0c5146" />


Now go to /.ssh folder and check the file

<img width="856" height="167" alt="image" src="https://github.com/user-attachments/assets/5c4c7800-4201-4992-922d-b91fc1efa548" />


once it is done, now give permission to user (being in the .ssh folder) to use the pem key file to login to the virtual machine using below command.
**chmod 500 prometheusvm_key.pem**


Now, using this command login to vm. Here the azureuser is the username you can find this in the above screenshot.
**ssh -i prometheusvm_key.pem azureuser@4.198.169.45**

After successfully logged into virtual machine you can verify that the username will change to virtual machine name as shown in below screenshot.

<img width="920" height="559" alt="image" src="https://github.com/user-attachments/assets/268cf4b8-d14c-463b-97c9-19e431030c12" />


## **Step3: Setup Agent**

Now Go to -> Azure DevOps portal -> then open your Project -> click on Project settings at bottom left corner. 

<img width="1825" height="840" alt="image" src="https://github.com/user-attachments/assets/bf2639d3-af2b-4aca-b5a8-e8e3fe978197" />

then go to -> agent pools -> click on add pool (top right corner) -> select self-hosted -> give a name for pool -> scroll down and then check mark the pipeline permission 'Grant access permission to all pipelines" -> click create.


<img width="1824" height="834" alt="image" src="https://github.com/user-attachments/assets/f255949a-a3bc-407b-bff2-218551fe3a74" />












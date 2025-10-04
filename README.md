# Azure-Linux-Virtual-Machine-Creation-Detailed-Guide
This Repo guides you through each step using images with markups for creating a linux virtual machine in Azure portal.
and also guides you how to login to the virtual machine using ssh key from your local command prompt or git.

Additionally i will guide you through steps for creating self-host agent for using it in Azure DevOps CICD for running pipeline. 

## **Let's get started**

**Step1: Create Virtual Machine**

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

<img width="1859" height="839" alt="image" src="https://github.com/user-attachments/assets/65493245-33d6-400c-960c-7cf76331e2a7" />


**Step2: Open the Git**

Now, go to downloads folder there you will see pem key file which was downloaded while creating virtual machine. 
copy this file and paste it in ~/.ssh folder









# Azure-Linux-Virtual-Machine-Creation-Detailed-Guide
This Repo guides you through each step using images with markups for creating a linux virtual machine in Azure portal.
and also guides you how to login to the virtual machine using ssh key from your local command prompt or git.

Additionally i will guide you through steps for creating self-host agent for using it in Azure DevOps CICD for running pipeline. 

## **Let's get started**

Go to -> **Azure portal** -> search **virtual machine** -> open **virtual machine** -> 

<img width="1919" height="566" alt="image" src="https://github.com/user-attachments/assets/f796b694-fe87-497c-824e-7048584c43ad" />



click create -> **virtual machine** -> give **resource group** name (else click create new) -> **virtual machine** name.

<img width="1748" height="780" alt="image" src="https://github.com/user-attachments/assets/a5859cb4-277b-40de-8405-188abf162e40" />



scroll down -> **image** choose **ubuntu server 22.04 LTS** -> **size** choose **Standard D2s_v3**

<img width="1861" height="839" alt="image" src="https://github.com/user-attachments/assets/f587d069-7462-40d5-94b7-abafbfb1933b" />



**authentication** type choose ssh public key -> click **review + create** -> **create**.

<img width="1840" height="774" alt="image" src="https://github.com/user-attachments/assets/d09a13a4-ddd0-4f4d-ab66-66abdeee3ea3" />



while creating virtual machine it will show a pop up window click on download the ssh key, the ssh public key will be downloaded to you local downloads folder, we will use this key while logging into the virtual machine.


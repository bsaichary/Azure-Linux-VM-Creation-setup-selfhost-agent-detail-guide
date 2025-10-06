# Azure-Linux-Virtual-Machine-Creation-Detailed-Guide
This Repo guides you through each step using images with markups for creating a linux virtual machine in Azure portal.
and also guides you how to login to the virtual machine using ssh key from your local command prompt or git.

Additionally i will guide you through steps for creating self-host agent for using it in Azure DevOps CICD for running pipeline. 

## **Let's get started**

## **Step1: Create Virtual Machine**

Go to -> **Azure portal** -> search **virtual machine** -> open **virtual machine** -> 

<img width="1919" height="566" alt="image" src="https://github.com/user-attachments/assets/f796b694-fe87-497c-824e-7048584c43ad" />


click create -> **virtual machine** -> give **resource group** name (else click create new) -> **virtual machine** name.

<img width="1748" height="780" alt="image" src="https://github.com/user-attachments/assets/a5859cb4-277b-40de-8405-188abf162e40" />


scroll down -> **image** choose **ubuntu server 22.04 LTS** -> **size** choose **Standard D2s_v3**

<img width="1861" height="839" alt="image" src="https://github.com/user-attachments/assets/f587d069-7462-40d5-94b7-abafbfb1933b" />


**authentication** type choose ssh public key -> click **review + create** -> **create**.

<img width="1236" height="818" alt="image" src="https://github.com/user-attachments/assets/24aa6315-2a20-42b7-bdea-1c4df2d0bb7f" />


while creating virtual machine it will show popup window click on download the ssh key, the ssh public key will be downloaded to you local downloads folder, we will use this key while logging into the virtual machine.

<img width="613" height="400" alt="image" src="https://github.com/user-attachments/assets/0ac3ba52-c3db-467e-9981-724869aafd7e" />


After creating virtual machine note down the public ip & username of virtual machine. it is mandatory for logging into vm.

<img width="1483" height="780" alt="image" src="https://github.com/user-attachments/assets/a851d593-0b97-4798-be19-98afcd50684e" />


## **Step2: Open the Git**

Open the Gitbash app for your laptop, go to downloads folder there you will see pem key file (prometheusvm_key.pem) which was downloaded while creating virtual machine. 

<img width="315" height="50" alt="image" src="https://github.com/user-attachments/assets/0c94ccdb-6565-4774-891f-eaa56aaebea5" />

s
It will look like this with you virtual machine name (monitoringvm_key.pem).  

<img width="1030" height="835" alt="image" src="https://github.com/user-attachments/assets/3ca68d4f-b67f-46e2-ab5f-1f7fc99b8110" />


copy this file and paste it in ~/.ssh folder

<img width="598" height="52" alt="image" src="https://github.com/user-attachments/assets/4163e7d4-7f53-4ee7-ab5a-3b8e18adf3d6" />


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


<img width="730" height="827" alt="image" src="https://github.com/user-attachments/assets/007b3976-d952-4e12-86a1-853007a48230" />

Now, open your created agentpool (this is the agent pool where your all the agent pools will be present) -> then click on agents (this is the place where all your agents will be listed) -> then click on create new agent.

<img width="1482" height="752" alt="image" src="https://github.com/user-attachments/assets/c5b8b580-3598-45a1-985a-5a9920dd6992" />


Click on Linux -> then copy button of the download agent.

<img width="1176" height="818" alt="image" src="https://github.com/user-attachments/assets/e43f4938-a232-45f1-88c3-0916bd777446" />

Go to -> Git bash where you have logged in to Azure virtual machine, now create a directory with a name agent. then go inside the directory and then paste the agent url with prefix curl -O to download the agent. and now using the list command (ll) we can see the downloaded agent file in .gz format (vsts-agent-linux-x64-4.261.0.tar.gz).
then we have to unzip the file and then start setup agent. use this command to unzip the file. ***tar zxvf vsts-agent-linux-x64-4.261.0.tar.gz*** 

<img width="710" height="235" alt="image" src="https://github.com/user-attachments/assets/2b74187c-af66-4bd8-a711-41daa5b103fb" />

It will download the agent into your agent directory. after downloading the agent we have to configure the agent. 
Now, with the help of config command we will configure the agent.
```
./config.sh
```
Once you run the config command it will ask you to accept the team explorer then type y then click enter, after that it will ask you to enter the server url (nothing but azure devops organization url), then it prompts for pat authentication just click enter then go to devops portal and click on user settings at top right corner beside user icon 

<img width="1890" height="503" alt="image" src="https://github.com/user-attachments/assets/04319d8f-7286-4411-a05e-d0fcfead8093" />


<img width="1804" height="676" alt="image" src="https://github.com/user-attachments/assets/ca472721-0f1a-49a6-a090-5c68ac3ccc53" />


<img width="949" height="365" alt="image" src="https://github.com/user-attachments/assets/83ab8323-68ed-4b0b-a0b6-8f6087a23d8f" />









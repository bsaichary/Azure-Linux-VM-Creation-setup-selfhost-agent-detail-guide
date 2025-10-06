# Azure-Linux-Virtual-Machine-Creation-Detailed-Guide
This Repo guides you through each step using images with markups for 
1. Creating a linux virtual machine in Azure portal.
2. Login to the virtual machine using ssh key from your local command prompt or git bash.
3. Setting up Self-host agent for using it in Azure DevOps CICD for running pipeline.
4. Installing Doker and Docker-compose and setting permission for using it to run CICD pipeline while creating Docker images.

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

Open the Gitbash app for your laptop, go to downloads folder there you will see pem key file (monitoringvm_key.pem) which was downloaded while creating virtual machine. 

<img width="315" height="50" alt="image" src="https://github.com/user-attachments/assets/0c94ccdb-6565-4774-891f-eaa56aaebea5" />

s
It will look like this with you virtual machine name (monitoringvm_key.pem).  

<img width="1291" height="807" alt="image" src="https://github.com/user-attachments/assets/306fc0e7-b056-4f5b-9b4b-57678dafdd26" />


copy this file and paste it in ~/.ssh folder

<img width="598" height="52" alt="image" src="https://github.com/user-attachments/assets/4163e7d4-7f53-4ee7-ab5a-3b8e18adf3d6" />


Now go to /.ssh folder and check the file

<img width="856" height="167" alt="image" src="https://github.com/user-attachments/assets/5c4c7800-4201-4992-922d-b91fc1efa548" />


once it is done, now give permission to user (being in the .ssh folder) to use the pem key file to login to the virtual machine using below command.
```
chmod 500 monitoringvm_key.pem
```


Now, using this command login to vm. Here the azureuser is the username you can find this in the above screenshot.
ensure you replace your detials with pem key file name, username and ip address in this command before running it.
```
ssh -i monitoringvm_key.pem azureuser@74.179.85.95
```

After successfully logged into virtual machine you can verify that the username will change to virtual machine name as shown in below screenshot.

<img width="852" height="666" alt="image" src="https://github.com/user-attachments/assets/5d155b1d-d1a6-46e9-b9da-ff247fc78b93" />


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
then we have to unzip the file and then start setup agent. use this command to unzip the file. 
```
tar zxvf vsts-agent-linux-x64-4.261.0.tar.gz
``` 

<img width="710" height="235" alt="image" src="https://github.com/user-attachments/assets/2b74187c-af66-4bd8-a711-41daa5b103fb" />

It will download the agent into your agent directory. after downloading the agent we have to configure the agent. 
Now, with the help of config command we will configure the agent.
```
./config.sh
```
Once you run the config command it will ask you to accept the team explorer then type y then click enter, after that it will ask you to enter the server url (nothing but azure devops organization url),  

<img width="1894" height="549" alt="image" src="https://github.com/user-attachments/assets/1f594a77-5e8d-4fc6-a32b-18c6c0909211" />


then it prompts for pat authentication just click enter then go to devops portal and click on user settings at top right corner beside user -> under that go to Personal Access Tokens.

<img width="949" height="365" alt="image" src="https://github.com/user-attachments/assets/83ab8323-68ed-4b0b-a0b6-8f6087a23d8f" />

In the Personal Access Tokens page click on new token at top right corner -> then provide name for pat token -> then check box the full access -> then click create.

<img width="1791" height="817" alt="image" src="https://github.com/user-attachments/assets/8da2425d-fab4-4f0b-9258-b5a93c9cab03" />

<img width="718" height="826" alt="image" src="https://github.com/user-attachments/assets/7b0a139d-cf26-4adf-bc5f-04f72359b2a9" />

then copy the pat and store it somewhere else for future use, once you close the pat token tab you wont be able see it again. 

<img width="702" height="810" alt="image" src="https://github.com/user-attachments/assets/4a1be19f-eb4b-41d4-83d3-03bcc4459dbd" />

Now, paste this pat token and click enter in git bash, after pasting the pat token it will ask you to enter the agent pool name which we have created (agentpool), enter it and click enter, then it will ask for agent name, give it of your choice then click enter then click enter and enter.

<img width="1891" height="673" alt="image" src="https://github.com/user-attachments/assets/af8a8664-3def-498a-9adf-a5a5c9bd8999" />


We have successfully configured the agent, now we should make the agent run. use below command to run agent, once the agent is up and running we can see it status as Listening to jobs and also we can verify the agent status as online with green colour dot in devops portal under agent which is under agentpools.
```
./run.sh
```

<img width="807" height="93" alt="image" src="https://github.com/user-attachments/assets/ac4d56bb-7b99-4bb0-b083-c0a917910a28" />

<img width="1863" height="828" alt="image" src="https://github.com/user-attachments/assets/ff9a3e0d-db91-42f3-9b72-2bbfd1342712" />

**Note: once you exit the gitbash the agent will stop running then again you have to run the ./run.sh command to make the agent run.**

## **Step4: Installing Docker**

First run this below command to uninstall all conflicting packages
```
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

<img width="1722" height="35" alt="image" src="https://github.com/user-attachments/assets/0e50aed6-a371-46d1-9b6c-7665cd9aa6ca" />


Now, we have setup apt repository for Docker.
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

then after completing the setup of apt repo for docker now we will Install docker packages
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```


<img width="1753" height="973" alt="image" src="https://github.com/user-attachments/assets/9e352b94-6294-4eb7-b994-9ce2f0b5a5e6" />

while installing it will say this operation will consume some dist space like 436mb then type enter this is to allow it to use the space on our disk.


after completing the installation of docker, we have to start the docker service and check the status using below commands.
```
sudo systemctl start docker
sudo systemctl status docker
```

<img width="1889" height="506" alt="image" src="https://github.com/user-attachments/assets/8cddb3b4-2c76-4676-990b-c3fee20ab45a" />


To verify the docker installation is successfull we can run the sample command hello-world image, docker will fetch that image from docker hub and show us. 
```
sudo docker run hello-world
```

<img width="1061" height="568" alt="image" src="https://github.com/user-attachments/assets/3416d49a-9d58-4bda-9679-a44662670ac6" />


## **Step5: Install Docker-compose**

To install docker-comose we need to run the below command.
```
sudo apt-get update
sudo apt-get install docker-compose-plugin
```
after insallation is completed check the status of docker-compose version
```
docker compose version
```

<img width="966" height="328" alt="image" src="https://github.com/user-attachments/assets/a2bd381a-945f-4142-9107-f8d9c9537430" />




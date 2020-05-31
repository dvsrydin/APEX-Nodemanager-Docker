# Supernode GUI Installation Guide & Support Documentation

### Important commands

#### Build & Start
docker-compose build --no-cache && docker-compose up -d
#### Reset (Delete) Containers
docker-compose down -v
#### Prune old container builds
docker system prune
#### Start - run this command in the Apex-Nodmanager-Docker directory
docker-compose start
#### Stop - run this command in the Apex-Nodmanager-Docker directory
docker-compose stop
#### See container logs
docker logs -f nodemanager
#### Bash into container
docker exec -it nodemanager /bin/bash

### Revision
| Revision History | Contributor | Date | Notes |
| --- | --- | --- | --- |
0.1	| Devious_One	| Jan 25, 2020	| Initial version 

### Table of Contents
Section 1: Server Configuration & Details  
Section 2: Supernode Server Setup (CLI)  
Section 3: Supernode Manager (GUI)  
Section 4: Troubleshooting  

# Section 1: Server Configuration & Details
The following server requirements are identified as the most current minimum requirements.  

### 1.1 Supernode System Specs
  * Minimum 8-Core Processor (16-Core
Recommended)
  * Minimum 16 GB RAM (32 GB Recommended)
  * 1 TB SSD (2 SSD Recommended)
  * Redhat, CentOS, Ubuntu
  * AWS or Azure Recommended
  * DDOS Protection 
 
# Section 2: Supernode Setup (CLI)
##  2.1 Architecture
<img src="https://miro.medium.com/max/761/1*OCIk1K1qr8ol-CaGMBcdTg.png"/>

## 2.2 Get Required Repositories
This section covers the basics for configuration of your server:  
**1.** Get Apex Node Manager Docker repo
  
`git clone https://github.com/APEX-Network/APEX-Nodemanager-Docker.git`

**2.** Get Apex Node Manager repo
  
`git clone https://github.com/yuomii/APEX-Nodemanager.git`


## 2.3 Build Docker
**Prerequisites:**

*Install Docker on your server: The following link provides a walkthrough for a complete install of Docker if not already installed on your server. 
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04*

  **1. Install Docker Compose**
  
`apt install docker-compose`


  **2. Build Application**
  
`docker-compose up -d --force-recreate`

  **3. Realtime view of logs**
  
`docker logs -f nodemanager`

  **4. Confirm both Docker containers are running**
  
 `docker container ls`

| Container Name | Status | 
|--- | --- |
Mongo | Up
NodeManager	| Up

To exit out of logs viewer, Ctrl+Z at any time


# Section 3. Supernode Manager GUI Setup
=====
The GUI should now be ready after you’ve built the dockers above.

GUI link: https://yourpublicIP:9100  

https://XXX.XXX.XXX.XXX:9100/

## 3.1 Registration & Login
### 3.1.1 Registration Page
The first time you visit the GUI, the registration page will be displayed.  Here you must enter:  
  *	Username
    *	*need to capture username requirements*
  *	Username is case-sensitive
  *	Password <need to capture password requirements>
  *	Repeat Password
 
Using your 2FA Authentication app, scan or manually enter the secret key.  

Note: There is no way to recover your password or 2FA if lost. Back it up by saving the QR code, secret key, or both.

### 3.1.2 Login Page
Once you've registered, you will always be taken directly to the login page. You will no longer see the new registration page. 
*insert picture of login page* 
 
## 3.2 Manager Configuration


### 3.2.1 Homepage
*insert picture of home page*
Welcome to the Apex Supernode Management Homepage! The map presented will show general locations of all Producing nodes once you've started the syncing process.  Before that, there are few things to setup and configure. 

### 3.2.2 Configuration Page
There are number of configurations required before you install & start your node.

#### A. GENERAL SETTINGS SECTION
Entering the Producer Private Key is optional.   

**Provide Key:**

Your node is only eligible to be a producer node when you provide your Producer Private Key. **Note:** The producer Key must be entered in HEX format.  
*Provide instructions to convert from WIF to HEX / and/or check if already in HEX format*  

**Do Not Provide Key:**

If you do not enter the Producer Private Key, your node will sync up with the chain, but your node is not eligible to be a producer.  

#### B. NETWORK SECTION
Declared IP is the only value that needs to be updated in this section.  Generally, your port will be 9090 unless you've made other configuration changes. 
 
#### C. KNOWN PEERS / SEED PEERS SECTION
Known Peers & Seed Peers will be provided by Apex configuration resources (via Apex Network Telegram Admins).  
Two Known peers & Two Seed peers must be provided. Generally, you can set:

  *	Known Peer 1 = Seed Peer 1 
  *	Known Peer 2 = 2 Seed Peer 2

**Note:** Port 9090 may not always be the correct port - adjust as necessary.
 
 
Lastly, Save configuration changes. 
 
Page will refresh and settings will be saved.  Review your changes to ensure they have entered correctly.
 
### 3.2.3 Node Page
The first time you visit the Node page, there will be no information or stats available.  There is a message "No installation found".  Before you begin the install, make sure you’ve properly completed and save the configuration settings.
 
  **1. Fill out the Git Commit Has or Branch**  
`master`
 
  **2.	Select the release version**  
`0.9.2`

  **3.	Click 'Install'**
The install & start buttons will become inactive indicating the installation has been initiated.

There is currently no status indicator within the GUI. Following along in the logs will show progress.  

The process will take 1-2 minutes.  

If you are following the terminal logs, you should see the following: 
 
> BUILD SUCCESSFUL in 1m 1s
> 3 actionable tasks: 3 executed
> 2020-01-24 02:59:12.693  INFO 49 --- [       Thread-3] app.process.ProcessExecutor              : Core build finished
> 2020-01-24 02:59:12.694  INFO 49 --- [       Thread-3] app.process.ProcessExecutor              : Copy new jar
> 2020-01-24 02:59:12.747  INFO 49 --- [       Thread-3] app.process.ProcessExecutor              : Installation finished
 
Once the logs files have indicated that the installation was successful, you can refresh the page.
 
The Supernode status will now indicate a status of 'Stopped'. The Apex core has been successfully installed, and is now ready to be started. 
 
 
After you’ve selected Start
  * The status will update to 'Running'
  * Your node should start syncing with the main chain.  Depending on the current block, this can take days.
 
### 3.2.4 Settings

#### A. Updating your Supernode Manager
When an update is available (via notification from the Developers) the update process requires steps both from the Supernode Manager (UI) & Docker (Server).
1 - Within the Supernode Manager UI -> Settings tab, click on 'Update'.
  Note: Please make sure your node is shut down before restarting the application via Docker
2 - Within the Supernode Manager UI -> Node tab, click on 'Stop'.  The page will refresh and identify that your Supernode is not currently running.
3 - Within your Server, navigate to the Apex-Supernode-Docker directory.  Run the following two commands. 
3.1 - docker-compose stop.
Note: Allow the stop process to fully complete.
3.2 - docker-compose start

After the Docker has been restarted, you will be logged out of the Supernode UI.  You should now see the updates. 

#### B. Change Password
To update your current password, enter your current password, your new password, and your new password again.  Click Change.  If successful, you will be logged out, and redirected back to the login page.  

If you have successfully updated your password, you will be logged out, and redirected to the login page. If you were unsuccessful in updating your password, the page will refresh and you will remain logged in.
 
#### C. Forgotten Password / Forgotten 2FA
There is currently no recovery / reset procedures for forgotten passwords or 2FA.  This requires a wipe/delete of the nodemanager user database.  See troubleshooting section for details on resetting this. 
 
# Section 4. Troubleshooting

## 4.1 Lost password / 2fa
There is currently no recovery / reset procedures for forgotten passwords or 2FA.  This requires a wipe/delete of the nodemanager database. Deleting the nodemanager user database will erase all stored user credentials. However, this action will not delete your current configurations settings.
 
*what happens to the Core / Sync'd data, etc.*
*what are the other ramifications of deleting the nodemanager*

**1.	Delete the Supernode application user database**
From the terminal, access the docker NODEMANAGER container
docker exec -it nodemanager /bin/bash
 
**2. Navigate to the root folder:**  
`cd ~`  
 
**3. Show contents of root:**  
`dir`  
 
**4. Delete the nodemanager database**  
`rm app-db.mv.db`
 
**5. Exit the Nodemanager container**  
`exit`

## 4.2 Firewall Settings
Docker will open the ports configured in the docker-compose.yml for you

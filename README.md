## Dot Marketplace Docker ##
## Setup ##
First, complete the basic Rust setup instructions. If you want to play at the code level.

If No, then plz follow this simple guide to make your life easy :)

Run in Docker

# Install Docker & Docker-Compose

First, install Docker and Docker Compose. Follow the basic installation guide [Docker](https://docs.docker.com/engine/install/) and [Docker Compose](https://docs.docker.com/compose/install/)

For a Windows Machine

[Follow the guide mentioned here](https://docs.docker.com/desktop/windows/install/)

Installation from the terminal on a Ubuntu/Linux Machine 

`curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`

`chmod +x /usr/local/bin/docker-compose`

# Docker quick guide

To check the compose version
```bash
docker-compose --version
```
To run the build

```bash
docker-compose up --build -d
``` 

To stop the service

```bash
docker-compose down
```

To view the installed images locally

```bash
docker images
```

To delete the images

```bash
docker rmi <IMAGE ID>
```

To get more idea about the project and the build please refer the link <To be added>

# Guide To Run All The Services At Once

Once this repo is cloned, follow the commands below to start all the services at once from the main project directory

```bash
docker-compose up --build -d
```
You will be able to see all the running services using 
```bash
docker ps
```
Each of these services will be running on the local system ports as below
1. dot_marketplace_frontend: Directly run the frontend to test out the application. [http://127.0.0.1:9001]
2. authentication_service: This is the api server to check the authentication service [http://127.0.0.1:7001]
3. marketplace_mongo: Mongodb for the application
4. dot_marketplace_node: Substrate based blockchain node, this can also be tested on the [polkadot js explorer](https://polkadot.js.org/apps/#/) Select local node to connect to the local running chain.[ws://127.0.0.1:9944]

To stop all the services
```bash
docker-compose down
```

# Guide To Run Each Of The Services Individually

Names of the individual service files
1. Blockchain Node: `tasking_backend.docker-compose.yml`
2. UI: `tasking_frontend.docker-compose.yml`
3. Auth Server: `authentication_service.docker-compose.yml`
4. Mongodb: `marketplace_mongo.docker-compose.yml`

To run the services individually 

```bash
docker-compose -f <file_name> up --build -d
```
To stop an individual service

```bash
docker-compose -f <file_name> down
```
# Individual Service Repos (To do a code walkthrough)
1. [Tasking Backend Node](https://github.com/WowLabz/tasking_backend.git)
2. [Tasking Frontend](https://github.com/WowLabz/tasking_frontend.git)
3. [Authentication Service](https://github.com/WowLabz/authentication_service.git)

# Container Instructions
In order to check for the status of the running node run 
```bash
docker-compose logs <CONTAINER ID>
```

# Run UI
You can access the frontend application on `http://127.0.0.1:9001`

![Screenshot_15](https://user-images.githubusercontent.com/11945179/131972401-6a700ce1-d938-45e2-931d-a50986daac12.png)

# Launch Interactive Bash Session with the Node
    
```bash
docker exec -it <CONTAINER ID> bash
``` 
|OR| 
```bash
docker exec -it <CONTAINER ID> /bin/sh
```
    
# Run Tests for the blockchain node

Enter into the interactive bash with the container id pertaining to dot_marketplace_node and run the following commands
    
`cargo test` (This will run all the test cases)
 
 `cargo test <test_name>` (For checking any specific test case)

# Interacting with Polkadot Js Apps Explorer
    
![BlocksFinality](https://user-images.githubusercontent.com/11945179/131971129-d166e10f-5efe-4d1a-8fab-082ba8a13a07.png)
    
To check the working of palletTasking go to Developers -> Extrinsics -> Submit the following Extrinsic -> palletTasking -> createTask (Starting Point, explore further we have worked on the full tasking lifecycle) 

![ChainExtrinsics](https://user-images.githubusercontent.com/11945179/131971070-580769be-7827-429e-8d9b-7216997813ca.png)
    
    
To read about the working of the pallet please refer the guide [Description](https://github.com/WowLabz/tasking_backend/tree/dev#readme)

# Note:
1. User will have to install the polkadot-js extension and create an account through the extension. [Link to the extension](https://polkadot.js.org/extension/)
2. Its preferred to use the chrome browser.
3. If the application is started using this docker repo, you will be able to access it at
```
http://localhost:9001/
```

# Functional Guide for Dot MarketPlace

* `Customer` Work Flow
    1. Create Task
    2. Approve Task

* `Worker` Work Flow
    1. Bid For Task
    2. Complete Task
    3. Provide Customer Ratings

1. User Sign Up
* User can choose to sign up either as a `Customer` or `Worker`
* `Customer` is one who wants to posts jobs/tasks that are needed to be completed
* `Worker` is one who bids for a job/tasks and see to its completion

* User is required to choose from the User Tags that are provided, multiple option can be choosen

![Screenshot_20211027_122755](https://user-images.githubusercontent.com/66478092/139015707-0e4d0f45-0c09-4102-be93-b80b0d49b730.png)

2. User Sign In
* User can sign in with the username (email) and password

3. DashBoard
* Once the user is logged in you will see an empty dashboad, user can create a new task & connect to the wallet

![Screenshot_20211027_100846](https://user-images.githubusercontent.com/66478092/139017058-75fee4ce-c1fa-4a89-a5d6-50d18eb6a479.png)

* Wallet Connection and creating an account
    - Click on add account and follow the steps below

![image (1)](https://user-images.githubusercontent.com/66478092/139018097-4b33be46-143d-40fc-9297-d42126da9237.png)

* Once the account is created you can connect the wallet with the application by clicking on `Connect Wallet` > `Polkaotdot-js`. Once clicked you will be able to see the account name and the balance

* Account Name is a dropdown from which you can choose any of the accounts

![Screenshot_20211027_125821](https://user-images.githubusercontent.com/66478092/139019829-fa26889e-b336-4121-9502-c9f661c5c486.png)

* You can now start with either work flow for `Customer` or `Worker` by choosing the defualt accounts `Alice` or `Bob`. You can use the connected account for all the transcations by requesting test tokens using `Air Drop`

4. Request `Air Drop` for test tokens

![Screenshot_20211027_130413](https://user-images.githubusercontent.com/66478092/139020631-293fef73-c088-41ba-831f-df42aa824b1f.png)

5. Create Task

* As a `Customer`, 
    - Choose account
    - Task Name & Task Cost
    - deadline for the task completion (days)
    - choose the nature of the task from the task tags
    - you can choose to upload any task related files

![Screenshot_20211027_130604](https://user-images.githubusercontent.com/66478092/139020871-0c48cd2f-7cd6-423c-b0ab-4301a0870754.png)

![Screenshot_20211027_130715](https://user-images.githubusercontent.com/66478092/139021065-a5c5ffcc-b1dd-49f7-ad1f-1fc95cd323ec.png)

* If you choose your own account you will get a pop up as below to authorize the transaction

![Screenshot_20211027_131031](https://user-images.githubusercontent.com/66478092/139021709-f6ae6ecb-3f03-41fd-bb8a-399f88a6f3fc.png)

* Notificatons are shown on the right for each transaction & the task is created

![Screenshot_20211027_131201](https://user-images.githubusercontent.com/66478092/139021812-6b327be5-acb9-4915-bbe1-23bc3e620e6d.png)

* You can click on the task card to see more details

![Screenshot_20211027_131348](https://user-images.githubusercontent.com/66478092/139022143-b4a92fce-b295-4b87-b098-08f70f8624fb.png)

* You can see the `task completion percentage` and the completed stages in the workflow
* When a task is created, amount equivalent to the `task cost` is locked into `escrow` from the `Customer's Account`
* Attachments can be downloaded by clicking on the respective attachment number

6. Bid Task

* As a `Worker`, 
    - Choose account

![Screenshot_20211027_132251](https://user-images.githubusercontent.com/66478092/139023517-55dca4c6-fec0-4664-a43a-889830b8f19a.png)

* Once the task is bidded you can see the status on the card change from `Open` to `InProgress`
* Along with the worker's name updated on the card

![Screenshot_20211027_132337](https://user-images.githubusercontent.com/66478092/139023624-fb543849-4556-4f97-a0d6-9e86a77266d1.png)

* On clicking the card you can now see that the same ammount as the `task cost` is a locked into `escrow` from the `Worker's Account`
* Total Escorw amount as shown below are from both `Customer` and `Worker`

![Screenshot_20211027_132714](https://user-images.githubusercontent.com/66478092/139024284-fb9320e8-75c0-43b5-8aa6-0e0996338af2.png)

7. Complete Task

* As a `Worker`, 
    - Choose account
    - upload any task related files

* On completion the staus will now be changed from `InProgress` to `PendingApproval`

![Screenshot_20211027_133413](https://user-images.githubusercontent.com/66478092/139025426-f40b05ce-832e-4e7e-9c60-2e596813edf3.png)

![Screenshot_20211027_133453](https://user-images.githubusercontent.com/66478092/139025526-828c8bbf-662c-4bfa-b1d1-52fa813b603a.png)

8. Approve Task

* As a `Customer`, 
    - Choose account
    - provide ratings for the worker

![Screenshot_20211027_133614](https://user-images.githubusercontent.com/66478092/139025747-ad59110a-11ab-4b7c-9106-0c8b158ed4ab.png)












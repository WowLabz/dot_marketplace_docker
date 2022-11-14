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
1. dot_marketplace_frontend: Directly run the frontend to test out the application. [http://127.0.0.1:8000]
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
4. [File Server](https://github.com/WowLabz/dot_marketplace_file_server.git)

In order to check for the status of the running node run 
```bash
docker-compose logs <CONTAINER ID>
```

# Run UI
You can access the frontend application on `http://127.0.0.1:8000`

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

# Note:
1. Users will have to install the polkadot-js extension and create an account through the extension. [Link to the extension](https://polkadot.js.org/extension/)
2. It's preferred to use the Google Chrome browser.
3. If the application is started using this docker repo, you will be able to access it at
```
http://localhost:8001/
```

# Functional Guide for Dot Marketplace

* `Customer` Workflow:
    1. Create Project
    2. Add Milestones To Project
    3. Add Project To Marketplace
    4. Accept Bid
    5. Approve Milestone
    6. Provide Worker Ratings

* `Worker` Workflow:
    1. Bid For Milestone
    2. Complete Milestone
    3. Provide Customer Ratings

* `Juror` Workflow:
    1. Cast Vote

### 1. User Sign Up
* Users can choose to sign up either as a `Customer` or a `Worker`.
* User is required to choose from the *user tags* that are provided, multiple options can be chosen.
* `Customer` is the one who wants to post tasks that are to be completed. `Worker` is the one who bids for tasks and works for its completion.

![Screenshot_20211027_122755](https://user-images.githubusercontent.com/66478092/139015707-0e4d0f45-0c09-4102-be93-b80b0d49b730.png)

### 2. User Sign In
* Users can sign in with the username (email) and password.

### 3. DashBoard
* Once the user is logged-in, they will see a dashboard and they can connect to the wallet and view all the milestones that have been created by multiple users.

![Screenshot_20211027_100846](https://user-images.githubusercontent.com/43837760/201646096-53935c49-8940-4e33-b692-775f05d42da5.png)

* Connecting the wallet by creating an account (as in the screenshot).


![image (1)](https://user-images.githubusercontent.com/66478092/139018097-4b33be46-143d-40fc-9297-d42126da9237.png)

* Once the account is created you can connect the wallet with the application by clicking on `Connect Wallet` > `Polkadot-js`. Once clicked you will be able to see the account name and the balance.

* Account Name is a drop down from which you can choose any of the accounts.

![Screenshot_20211027_125821](https://user-images.githubusercontent.com/43837760/201646808-ea8c06b3-ded9-4e93-b7c2-d62478b2c52e.png)

* You can now start with workflow for either `Customer` or `Worker` by choosing the default accounts `Alice` or `Bob`.
* Otherwise you can connect your own account and request test tokens through `Air Drop` to perform transactions.

### 4. Request `Air Drop` for test tokens

![Screenshot_20211027_130413](https://user-images.githubusercontent.com/43837760/201646955-b8ae9e58-0c5d-4f5e-b3f2-660082f69581.png)

### 5. Search Milestones
* As a `Worker`: 
    - Provide a specific criteria for search

![Screenshot_AdvanceSearch1](https://user-images.githubusercontent.com/43837760/201657120-cd62e376-79b2-44b7-8aa2-460cfc762cfb.png)

![Screenshot_AdvanceSearch1](https://user-images.githubusercontent.com/43837760/201657135-5f45e4d3-b4a3-4b02-8665-955d3a0b6f28.png)

![Screenshot_AdvanceSearch1](https://user-images.githubusercontent.com/43837760/201657148-b595bb61-8e70-4ef1-9167-9f4e78f7d3fd.png)


### 5. User Dashboard

* Users can click on the 'User Dashboard' button on the main dashboard to redirect to the `User Dashboard` that provides the functionality to manage all the projects. 
* Inilitally user will see an empty dashboard and choose to create a new project.

![Screenshot_UserDashboard](https://user-images.githubusercontent.com/43837760/201647203-bcde7b74-7cdf-4eed-8c29-bea6c1c78dcc.png)

### 6. Create Project

* As a `Customer`:
    - Project Name & Project Tags
    - Add Milestone
 
![Screenshot_CreateProject1](https://user-images.githubusercontent.com/43837760/201647462-1696c2f8-ec77-4168-8cfe-b8bfb9db83b6.png)

![Screenshot_CreateProject2](https://user-images.githubusercontent.com/43837760/201647615-42a44ab4-4303-4b1b-bfa2-acd5575d1943.png)

![Screenshot_CreateProject3](https://user-images.githubusercontent.com/43837760/201648346-dc96182a-47cf-4d4c-b1b6-4740f803d5cb.png)


### 7. Add Milestone

* Milestones can be added while creating the project(a minimum of one has to be added while creating the project) and/or before adding the project to the marketplace
* As a `Customer`:
    - Milestone Name & Milestone Cost
    - Choose the nature of the milestone from the tags
    - Deadline for completion (days)
    - You can choose to upload milestone related files
* While adding milestone(s) to the project, an amount equivalent to the `Milestone Cost` is locked into the `escrow` from the `Customer's Account`.

![Screenshot_AddMilestone1](https://user-images.githubusercontent.com/43837760/201647825-077357e2-142e-4a35-93bc-f1fbdb1c97d1.png)

![Screenshot_AddMilestone3](https://user-images.githubusercontent.com/43837760/201648008-f012655c-2916-4063-8815-ebb9d109b0ee.png)

![Screenshot_AddMilestone4](https://user-images.githubusercontent.com/43837760/201648034-05b4bbb5-b293-4362-864b-92da060a0485.png)


* You can click on the project card to see more details.

![Screenshot_Project1MoreDetails1](https://user-images.githubusercontent.com/43837760/201649567-55c51afc-8816-4303-99cd-7e2fb7722c2d.png)


* You can see the details about a project in the accordion provided. You can click on each individual milestone to see full details.

![Screenshot_Project1MoreDetails1](https://user-images.githubusercontent.com/43837760/201649584-496d575d-b42b-4999-8e52-f15d826fa9df.png)


### 8. Add Project To Marketplace

* As a `Customer`, if you think the project is ready to be submitted, add the project to the marketplace. Otherwise, you can make changes to the project if desired.

![Screenshot_AddProjectToMarketplace](https://user-images.githubusercontent.com/43837760/201648525-f4ae1847-1b8c-4b83-ba51-23258ae10c16.png)


### 9. Bid Milestone

* As a `Worker` (inside main dashboard):
    - Click on the milestone card
    - Select the milestone and click on `Bid`
* While bidding on a milestone, amount equivalent to `Milestone Cost` is locked into the `escrow` from `Worker's Account`.
* Once the bid is placed successfully, wait for the `Customer` to accept your bid.

![Screesnshot_BidMilestoneDashboard](https://user-images.githubusercontent.com/43837760/201654195-c8e24071-058b-4583-8e04-6d4eab222207.png)


![Screenshot_BidMilestone](https://user-images.githubusercontent.com/43837760/201650196-d24341b3-e167-41e0-81eb-6a4723657073.png)


### 10. Accept Bid

* As a `Customer`:
    - Accept a bid most suitable for the milstone
* Once the bid has been accepted, you can see the status on the card change from `Open` to `InProgress`, as well as the worker's name updated on the card.
* All the other bids are rejected and the amount locked into the escrow is returned back to their account.


![Screenshot_ShowBidders](https://user-images.githubusercontent.com/43837760/201650518-d95a299c-8415-4601-9dfd-d500c1186673.png)

![Screenshot_AcceptBid](https://user-images.githubusercontent.com/43837760/201650527-052b24a6-acdc-4e1b-b7b6-dcbd960424b4.png)


### 11. Complete Milestone

* As a `Worker`: 
    - Upload any milestone related files and complete milestone
* On completion, the status will change from `InProgress` to `PendingApproval`.

![Screenshot_CompleteMilestone1](https://user-images.githubusercontent.com/43837760/201652247-df2b5147-6f4e-4e35-a2b1-45a499f41b21.png)

![Screenshot_CompleteMilestone2](https://user-images.githubusercontent.com/43837760/201652269-24e79c6d-9ae6-4c81-a38f-3234177cac86.png)

![Screenshot_CompleteMilestone3](https://user-images.githubusercontent.com/43837760/201652165-2f50e21f-df13-45e5-9c93-4ea86562885d.png)

![Screenshot_PendingApproval](https://user-images.githubusercontent.com/43837760/201652086-00869b5e-89ab-4adb-8247-0a59ebd056c7.png)

### 12. Approve Milestone

* As a `Customer`:
    - Provide rating for the worker
    
![Screenshot_ApproveOrDisapprove](https://user-images.githubusercontent.com/43837760/201651955-40edbeb8-7485-4d40-90b1-99cc1dbc86c4.png)

![Screenshot_ApproveMilestone](https://user-images.githubusercontent.com/43837760/201651972-3719e813-569a-4882-b6c3-b82fccfb2ec2.png)


### 13. Provide Customer Ratings:

* As a `Worker`:
    - Provide ratings for the customer
![Screenshot_ProvideRatingOrDisapproveRAting](https://user-images.githubusercontent.com/43837760/201651775-3692eabc-db06-404d-86b7-dad6575302bb.png)

![Screenshot_ProvideCustomerRating](https://user-images.githubusercontent.com/43837760/201651788-28e1b33d-5f61-4d4d-9448-a632b54a3dcb.png)


### 14. Close Milestone

* As a `Customer`:
    - Close Milestone
* Once milestone has been closed, the amount will be released from the escrow.
* `Customer` will be debited with the amount for the `milestone cost`.
* `Worker` will be credited with the amount for the `milestone cost + amount he had locked into escrow`.
* The milestone is now `Completed`.

![Screenshot_CloseMilestoneOrDisapproveRating](https://user-images.githubusercontent.com/43837760/201651617-e526e13c-24c7-4342-b3b2-e8ddbc9a24fa.png)

![Screenshot_MilestoneCompleted](https://user-images.githubusercontent.com/43837760/201651626-3d8ffc09-9b6d-438e-b94f-4ed8ce83c25a.png)


### 15. Close Project
* A project can be closed if all the milestones for the project are `Completed` or all the milestones for the project are in state `Open`.

![Screenshot_CloseProject](https://user-images.githubusercontent.com/43837760/201651516-862799dd-6416-48a6-b932-4b55ded4fcfa.png)

### 16. Disapprove Rating
* As a `Customer`, you can disapprove with the kind of work done by the `Worker` or by rating provided by the `Worker`.

* As a `Worker`, you can disapprove with the rating provided by the `Customer`.

![Screenshot_DisapproveRatingCustomer](https://user-images.githubusercontent.com/43837760/201709064-e8289b50-71f8-4aea-ba53-099c92697b45.png)

![Screenshot_DisapproveRatingWorker](https://user-images.githubusercontent.com/43837760/201709210-dc9044de-7335-4cb9-9e02-7bddbdbc0624.png)


* After disapproving, you can the status of the milestone change to `Dispute Raised`.

![Screenshot_DisputeRaisedCustomer](https://user-images.githubusercontent.com/43837760/201709592-75bad141-1d87-4e08-a26e-bbb63eef0f7d.png)

![Screenshot_DisputeRaisedWorker](https://user-images.githubusercontent.com/43837760/201709775-48116969-cc06-4a05-85a4-048b4b37b42a.png)


* You can see the details about the dipute by clicking the `Show Court` button.

![Screenshot_CourtDetails](https://user-images.githubusercontent.com/43837760/201709322-65491452-515a-4dd4-8eac-e8aa368cc6e8.png)


### 17. Cast Vote
* As a `Juror` you cast your vote by providing:
    - Support to either `Worker` or `Customer`
    - Rating for `Worker`
    - Rating for `Customer`

![Screenshot_JurorCastVote](https://user-images.githubusercontent.com/43837760/201707966-64adbb30-ccf3-480f-b226-966c9a302359.png)

![Screenshot_Voting](https://user-images.githubusercontent.com/43837760/201708369-7b431a93-ece9-4509-86f1-0d88901a3569.png)

![Screenshot_AfterJurorCastVote](https://user-images.githubusercontent.com/43837760/201708674-dc57c811-98de-4050-852d-3ee581eb0211.png)


* As a `Sudo Juror` you cast your vote if the `Juror(s)` fail to cast their vote in a particular period of time, or in case of a tie between the votes.

![Screenshot_SudoJurorCastVote](https://user-images.githubusercontent.com/43837760/201708131-c2e39af0-dde1-420c-9736-ac9443fa5b08.png)

![Screenshot_Voting](https://user-images.githubusercontent.com/43837760/201708369-7b431a93-ece9-4509-86f1-0d88901a3569.png)

![Screenshot_AfterSudoJurorCastVote](https://user-images.githubusercontent.com/43837760/201708868-b5b11d52-4269-4742-8d10-011a738be1c9.png)



### 16. User Logout

* Users can logout from the option in the header.

![Screenthost_LogOut](https://user-images.githubusercontent.com/43837760/201651440-978973c5-a71d-4a38-83e1-c7813a6fcc21.png)


To read about the working of the pallet please refer the guide [Description](https://github.com/WowLabz/tasking_backend/tree/dev#readme)

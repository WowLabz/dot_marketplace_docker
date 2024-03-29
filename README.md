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
5. IPFS File Server: `dot_marketplace_file_server.docker-compose.yml`

To run the services individually 

```bash
docker-compose -f <file_name> up --build -d
```
To stop an individual service

```bash
docker-compose -f <file_name> down
```
# Individual Service Repos (To do a code walkthrough)
1. [Tasking Backend Node](https://github.com/WowLabz/dot-marketplace-v2/tree/Phase3_Milestone3)
2. [Tasking Frontend](https://github.com/WowLabz/tasking_frontend/tree/Phase3_Milestone3)
3. [Authentication Service](https://github.com/WowLabz/authentication_service/tree/version/2.0)
4. [IPFS File Server](https://github.com/WowLabz/dot_marketplace_file_server/tree/version/1.00)

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

# Note:
1. Users will have to install the polkadot-js extension and create an account through the extension. [Link to the extension](https://polkadot.js.org/extension/)
2. It's preferred to use the Google Chrome browser.
3. If the application is started using this docker repo, you will be able to access it at
```
http://localhost:9001/
```

## Video Demonstrations

1. Dot Marketplace - [Regular Task Workflow](https://user-images.githubusercontent.com/66478092/210616793-d55dabcb-0e8e-4860-a70e-3f40c80985f0.mp4)
2. [Court Dispute Resolution](https://user-images.githubusercontent.com/66478092/210618245-9f703673-cbd0-4627-8094-f1cf87625c3e.mp4)
3. [Court Sudo Juror](https://user-images.githubusercontent.com/66478092/210618324-13903436-4293-4714-9fc1-8aad3369ab95.mp4)
4. Backend Extrincis: The video demonstrates the flow of tasking backend which was created as a part of Phase 3 but has now been upgraded to milestone based submissions. [Video demo in with polkadot.js explorer connected to the node](https://user-images.githubusercontent.com/43837760/202637994-08705bb3-b99b-4f95-a828-381584d513d9.mp4)
5. Backend Decentralized Court workflow testing on Polkadot.js explorer: A functional demo of the court system when a publisher disapproves a milestone [Video demo in with polkadot.js explorer connected to the node](https://user-images.githubusercontent.com/43837760/202639155-419220ca-d0f6-46f4-8d9a-ad1c0678fecd.mp4)

<br>

## Dencetralized Court (Milestone Based)
1. The court caters to the Web3 space and hence by default becomes an autonomous entity run by the people.
2. It is designed in a way which resembles an actual offline court that helps in settling long term or short term disputes.
3. The disputes that we have thought of covering with this court is milestone based.
4. In the beginning there are 2 entities - a. The Customer b. Worker.
5. The customer is the entity that puts up work on the platform holding a specific amount for the work done as reward.
6. The worker is the entity that takes up the work for the customer in a hope to complete it in a given time frame.
7. When a case is registered for a specific dispute over a task / milestone.
8. Potential Jurors are selected based on their ratings (which it is set to 4 and above) and matching task tags. Each of them receive notification to accept/decline jury duty. For testing we have set a few accounts with predefined data at genesis [here](https://github.com/WowLabz/dot-marketplace-v2/blob/Phase3_Milestone3/node/src/chain_spec.rs#L150-L208).
9. The decision to be part of the jury is 1 day (1 era) or 14_400 slots i.e. 24 hours. However, for the purpose of testing it has been set to 5 blocks [source code](https://github.com/WowLabz/dot-marketplace-v2/blob/Phase3_Milestone3/pallets/pallet-tasking/src/lib.rs#L1972-L1996).
10. Once the day to become a juror has passed. Its not possible to be part of the jury for any respective case. Instead a Sudo juror is selected from a registered pool/council who are part of the chain.
11. Potential Juror can accept the jury duty and become an active juror by casting the vote and providing the ratings for both customer and worker.
12. There is limit set on how many jurors can take part. 2 jurors per case based on first come first serve basis.
13. Once the case begins/accepted, the jurors have 2 eras (2 days) to evaluate the work done & cast their votes to either of the parties i.e. the customer or worker. However, for testing purposes the duration is for 10 blocks.
14. Once all the votes have been cast by the participating jurors, the winner is decided and the amount is transferred to the winner automatically via the escrow.
15. If the winner is the customer, the customer doesn't have to pay anything to the worker.
16. If the winner is the worker, the reward amount from the escrow goes to the worker.
17. The jurors also get a share (this can be configured) for participating. The court fees is 30% of the total cost, which is divided equally among the final jurors.
18. If no jurors decide on participating, the process for selection is run for 3 more eras.
19. Even in those 3 eras there is no juror, then a Sudo juror is selected which is part of the ecosystem and his / her decision is not bound by time.
20. The Sudo juror is selected using the Fischer-Yates modern method & Linear Congruential Generator.


# Functional Guide for Dot Marketplace

* `Customer` Workflow:
    1. Create Project
    2. Add Milestones to Project
    3. Add Project to Marketplace
    4. Accept Bid
    5. Approve Milestone
    6. Provide Worker Ratings
    7. Close Milestone
    8. Close Project
    9. Disapprove Milestone
    10. Disapprove Rating
    11. Raise Dispute

<br />

* `Worker` Work Flow:
    1. Bid For Milestone
    2. Complete Milestone
    3. Provide Customer Ratings
    4. Disapprove Rating
    5. Raise Dispute

<br>

* `Juror` Work Flow:
    1. Accept Jury Duty

<br>


### 1. User Sign Up
* Users can choose to sign up either as a `Customer` or a `Worker`.
* User is required to choose from the *user tags* that are provided, multiple options can be chosen.
* `Customer` is the one who wants to post tasks that are to be completed. `Worker` is the one who bids for tasks and works for its completion.

![Screenshot_20211027_122755](https://user-images.githubusercontent.com/66478092/139015707-0e4d0f45-0c09-4102-be93-b80b0d49b730.png)

### 2. User Sign In
* Users can sign in with the username (email) and password.

### 3. DashBoard
* Once the user is logged-in, they will see a dashboard and they can connect to the wallet and view all the milestones that have been created by multiple users.

![image](https://user-images.githubusercontent.com/57192661/201854016-32689c0b-d1f2-4032-9b04-3a313be796b5.png)

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
* The search functionality is to find projects with one or more milestones, and the worker can use this search bar for accessing all of them based on a specific criteria provided by the worker himself / herself.

|Screenshot 1|Screenshot 2|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201657120-cd62e376-79b2-44b7-8aa2-460cfc762cfb.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201657135-5f45e4d3-b4a3-4b02-8665-955d3a0b6f28.png)|

|Screenshot 3|
|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201657148-b595bb61-8e70-4ef1-9167-9f4e78f7d3fd.png)|

### 6. User Dashboard

* Users can click on the 'User Dashboard' button on the main dashboard to redirect to the `User Dashboard` that provides the functionality to manage all the projects. 
* Inilitally user will see an empty dashboard and choose to create a new project.

![Screenshot_UserDashboard](https://user-images.githubusercontent.com/43837760/201647203-bcde7b74-7cdf-4eed-8c29-bea6c1c78dcc.png)

### 7. Create Project (by the customer)

* Mandatory fields:
    - Project Name & Project Tags
    - Add Milestone
 
![Screenshot_CreateProject1](https://user-images.githubusercontent.com/43837760/201647462-1696c2f8-ec77-4168-8cfe-b8bfb9db83b6.png)

### 7a. Add Milestone to a project (by the customer)

* Milestones can be added while creating the project (a minimum of one has to be added while creating the project) and/or before adding the project to the marketplace
* Mandatory fields:
    - Milestone Name & Milestone Cost
    - Choose the nature of the milestone from the tags
    - Deadline for completion (days)
    - You can choose to upload milestone related files
* While adding milestone(s) to the project, an amount equivalent to the `Milestone Cost` is locked into the `escrow` from the `Customer's Account`.

|Screenshot 1|Screenshot 2|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201647825-077357e2-142e-4a35-93bc-f1fbdb1c97d1.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201648008-f012655c-2916-4063-8815-ebb9d109b0ee.png)|

|Screenshot 3|Screenshot 4|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201648034-05b4bbb5-b293-4362-864b-92da060a0485.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201647615-42a44ab4-4303-4b1b-bfa2-acd5575d1943.png)|

* Final project with one / more milestones

![Screenshot_CreateProject3](https://user-images.githubusercontent.com/43837760/201648346-dc96182a-47cf-4d4c-b1b6-4740f803d5cb.png)

* You can click on the project card to see more details.

![Screenshot_Project1MoreDetails1](https://user-images.githubusercontent.com/43837760/201649567-55c51afc-8816-4303-99cd-7e2fb7722c2d.png)

* You can click on each individual milestone to see full details.

![Screenshot_Project1MoreDetails1](https://user-images.githubusercontent.com/43837760/201649584-496d575d-b42b-4999-8e52-f15d826fa9df.png)


### 8. Add Project To Marketplace (by the customer)

* If you think the project is ready to be submitted, add the project to the marketplace.

![Screenshot_AddProjectToMarketplace](https://user-images.githubusercontent.com/43837760/201648525-f4ae1847-1b8c-4b83-ba51-23258ae10c16.png)


### 9. Bid for Milestone (by the worker)

* Inside main dashboard, click on the milestone card and select the milestone for which the worker wants to `Bid`.
* While bidding on a milestone, amount equivalent to `Milestone Cost` is locked into the `escrow` from `Worker's Account`.
* Once the bid is placed successfully, wait for the `Customer` to accept your bid.

|Screenshot 1|Screenshot 2|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201654195-c8e24071-058b-4583-8e04-6d4eab222207.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201650196-d24341b3-e167-41e0-81eb-6a4723657073.png)|


### 10. Accept Bid (by the customer)

* Accept a bid most suitable for the milstone.
* Once the bid has been accepted, you can see the status on the card change from `Open` to `InProgress`, as well as the worker's name updated on the card.
* All the other bids are rejected and the amount locked into the escrow is returned back to their account.

|Screenshot 1|Screenshot 2|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201650518-d95a299c-8415-4601-9dfd-d500c1186673.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201650527-052b24a6-acdc-4e1b-b7b6-dcbd960424b4.png)|


### 11. Complete Milestone (by the worker)

* Upload the milestone related file(s) and click on complete milestone.
* On completion, the status will change from `InProgress` to `PendingApproval`.

|Screenshot 1|Screenshot 2|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201652247-df2b5147-6f4e-4e35-a2b1-45a499f41b21.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201652269-24e79c6d-9ae6-4c81-a38f-3234177cac86.png)|

|Screenshot 3|Screenshot 4|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201652165-2f50e21f-df13-45e5-9c93-4ea86562885d.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201652086-00869b5e-89ab-4adb-8247-0a59ebd056c7.png)|

### 12. Approve Milestone (by the customer)

* Provide a suitable rating for the worker according to the work done by the worker.

|Screenshot 1|Screenshot 2|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201651955-40edbeb8-7485-4d40-90b1-99cc1dbc86c4.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201651972-3719e813-569a-4882-b6c3-b82fccfb2ec2.png)|

### 13. Provide Customer Rating (by the worker)

* Provide rating for the customer.

|Screenshot 1|Screenshot 2|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201651775-3692eabc-db06-404d-86b7-dad6575302bb.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201651788-28e1b33d-5f61-4d4d-9448-a632b54a3dcb.png)|

### 14. Close Milestone (by the customer)

* Once milestone has been closed, the amount is released from the escrow.
* `Customer` is debited with the amount for the `milestone cost`.
* `Worker` is credited with the cumulative cost for completion of the milestone + the worker's initial bid amount locked in escrow.
* The status of milestone after completion is `Completed`.

|Screenshot 1|Screenshot 2|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201651617-e526e13c-24c7-4342-b3b2-e8ddbc9a24fa.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201651626-3d8ffc09-9b6d-438e-b94f-4ed8ce83c25a.png)|

### 15. Close Project
* A project can be closed if all the milestones for the project are `Completed` or all the milestones for the project are in state `Open`.

![Screenshot_CloseProject](https://user-images.githubusercontent.com/43837760/201651516-862799dd-6416-48a6-b932-4b55ded4fcfa.png)


## The decentralized court can be now triggered on every milestone.

### 16. Disapprove Rating
* As a `Customer`, you can disapprove with the kind of work done by the `Worker` or by rating provided by the `Worker`.

* As a `Worker`, you can disapprove with the rating provided by the `Customer`.

|Screenshot 1|Screenshot 2|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201709064-e8289b50-71f8-4aea-ba53-099c92697b45.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201709210-dc9044de-7335-4cb9-9e02-7bddbdbc0624.png)|

* After disapproving, the status of the milestone is changed to `Dispute Raised`.

|Screenshot 1|Screenshot 2|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201709592-75bad141-1d87-4e08-a26e-bbb63eef0f7d.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201709775-48116969-cc06-4a05-85a4-048b4b37b42a.png)|

* You can see the details about the dipute by clicking the `Show Court` button.

![Screenshot_CourtDetails](https://user-images.githubusercontent.com/43837760/201709322-65491452-515a-4dd4-8eac-e8aa368cc6e8.png)

### 17. Cast Vote
* As a `Juror` you cast your vote by providing:
    - Support to either `Worker` or `Customer`
    - Rating for `Worker`
    - Rating for `Customer`
    
|Screenshot 1|Screenshot 2|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201707966-64adbb30-ccf3-480f-b226-966c9a302359.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201708369-7b431a93-ece9-4509-86f1-0d88901a3569.png)|

|Screenshot 3|
|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201708674-dc57c811-98de-4050-852d-3ee581eb0211.png)|

* As a `Sudo Juror` you cast your vote if the `Juror(s)` fail to cast their vote in a particular period of time, or in case of a tie between the votes.

|Screenshot 1|Screenshot 2|
|:-:|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201708131-c2e39af0-dde1-420c-9736-ac9443fa5b08.png)|![Screenshot](https://user-images.githubusercontent.com/43837760/201708369-7b431a93-ece9-4509-86f1-0d88901a3569.png)|

|Screenshot 3|
|:-:|
|![Screenshot](https://user-images.githubusercontent.com/43837760/201708868-b5b11d52-4269-4742-8d10-011a738be1c9.png)|

### 16. User Logout

* Users can logout from the option in the header.

![Screenthost_LogOut](https://user-images.githubusercontent.com/43837760/201651440-978973c5-a71d-4a38-83e1-c7813a6fcc21.png)

To read about the working of the pallet please refer the guide [Description](https://github.com/WowLabz/tasking_backend/tree/dev#readme)

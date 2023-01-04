## Dot Marketplace Docker ##
## Setup ##
First, complete the basic Rust setup instructions. If you want to play at the code level. \
If no, then please follow this simple guide to make your life easy :+1:

## Install Docker & Docker-Compose

First, install Docker and Docker Compose. Follow the basic installation guide for [Docker](https://docs.docker.com/engine/install/) and [Docker Compose](https://docs.docker.com/compose/install/)

For a Windows Machine : [Follow the guide mentioned here](https://docs.docker.com/desktop/windows/install/)

Installation from the terminal on a Ubuntu / Linux machine 

```shell
$ curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
```shell
$ chmod +x /usr/local/bin/docker-compose
```

## Docker guide

Clone the repo for Phase 3 [ Milestone 2 ] [Dot Marketplace Docker](https://github.com/WowLabz/dot_marketplace_docker/tree/Phase3_Milestone2)

```shell
# To check the compose version
$ docker-compose --version
```

```shell
# To run the build
$ docker-compose up --build -d
```

```shell
# To stop the service
$ docker-compose down
```

```shell
# To view the installed images locally
$ docker images
```

```shell
# To delete the images
$ docker rmi <IMAGE ID>
```

>After building the image, you can also view it on polkadot.js explorer via local node

<br>

## Functional Guide for Dot Marketplace

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

## Migration from Tasks to Milestone based Projects

* >Video  walkthrough  
The video demonstrates the flow of tasking backend which was created as a part of Phase 2 but has now been upgraded to milestone based submissions. \
[Video demo in with polkadot.js explorer connected to the node](https://user-images.githubusercontent.com/43837760/202637994-08705bb3-b99b-4f95-a828-381584d513d9.mp4)


## Dencetralized Court
1. The court caters to the Web3 space and hence by default becomes an autonomous entity run by the people.
2. It is designed in a way which resembles an actual offline court that helps in settling long term or short term disputes.
3. The disputes that we have thought of covering with this court is milestone based.
4. In the beginning there are 2 entities - a. The Customer b. Worker.
5. The customer is the entity that puts up work on the platform holding a specific amount for the work done as reward.
6. The worker is the entity that takes up the work for the customer in a hope to complete it in a given time frame.
7. When a case is registered for a specific dispute over a task / milestone.
8. Potential Jurors are selected based on their ratings (which it is set to 4 and above) and matching task tags. Each of them receive notification to accept/decline jury duty. For testing we have set a few accounts with predefined data at genesis [here](https://github.com/WowLabz/dot-marketplace-v2/blob/Phase3_Milestone2/node/src/chain_spec.rs#L150-L232).
9. The decision to be part of the jury is 1 day (1 era) or 14_400 slots i.e. 24 hours. However, for the purpose of testing it has been set to 5 blocks [source code](https://github.com/WowLabz/dot-marketplace-v2/blob/Phase3_Milestone2/pallets/pallet-tasking/src/lib.rs#L2124-L2153).
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

## Decentralized Court workflow testing on Polkadot.js explorer 

* >Video  walkthrough \
A functional demo of the court system when a publisher disapproves a milestone\
[Video demo in with polkadot.js explorer connected to the node](https://user-images.githubusercontent.com/43837760/202639155-419220ca-d0f6-46f4-8d9a-ad1c0678fecd.mp4)

<br>

To read about the working of the pallet please refer the guide [Description](https://github.com/WowLabz/dot-marketplace-v2/blob/main/README.md)


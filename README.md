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

* `Worker` Work Flow:
    1. Bid For Milestone
    2. Complete Milestone
    3. Provide Customer Ratings
    4. Disapprove Rating
    5. Raise Dispute

* `Juror` Work Flow:
    1. Accept Jury Duty

<br>

## Migration from Tasks to Milestone based Projects

* >Video  walkthrough \ 
The video demonstrates the flow of tasking backend which was created as a part of Phase 2 but has now been upgraded to milestone based submissions. \
[Video demo in with polkadot.js explorer connected to the node](https://user-images.githubusercontent.com/43837760/202637994-08705bb3-b99b-4f95-a828-381584d513d9.mp4)


## Decentralized Court workflow testing on Polkadot.js explorer 

* >Video  walkthrough \
A functional demo of the court system when a publisher disapproves a milestone\
[Video demo in with polkadot.js explorer connected to the node](https://user-images.githubusercontent.com/43837760/202639155-419220ca-d0f6-46f4-8d9a-ad1c0678fecd.mp4)

<br>

To read about the working of the pallet please refer the guide [Description](https://github.com/WowLabz/dot-marketplace-v2/blob/main/README.md)


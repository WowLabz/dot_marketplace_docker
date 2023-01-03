FROM node:lts-alpine3.17

RUN apk update \
    && apk add git

RUN git clone --single-branch -b Phase3_Milestone3 https://github.com/WowLabz/tasking_frontend.git

WORKDIR /tasking_frontend

RUN yarn install 
RUN yarn add jquery 
RUN yarn add popper.js

EXPOSE 9001

CMD [ "yarn", "start", "build:docker" ]
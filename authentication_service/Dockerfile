FROM rust:1.54

RUN apt-get update \
    && apt-get install -y git

RUN git clone --single-branch -b version/2.0 https://github.com/WowLabz/authentication_service.git
WORKDIR /authentication_service

RUN cargo build 
EXPOSE 7001
CMD [ "cargo", "run" ]
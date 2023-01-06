FROM rust:1.63.0

RUN apt-get update \
    && apt-get install -y git

RUN git clone --single-branch -b version/1.00 https://github.com/WowLabz/dot_marketplace_file_server.git
WORKDIR /dot_marketplace_file_server

RUN cargo build 
EXPOSE 8001
CMD [ "cargo", "run" ]
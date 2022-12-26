FROM paritytech/ci-linux:production AS builder

RUN apt-get update \
    && apt-get install -y git

RUN git clone --single-branch -b Phase3_Milestone2 https://github.com/WowLabz/dot-marketplace-v2.git

WORKDIR /builds/dot-marketplace-v2
# RUN rustup update
# installing rust version 1.58.0-nightly
RUN rustup install nightly-2021-11-01
# setting rust default version as 1.58.0-nightly
RUN rustup default nightly-2021-11-01
RUN rustup target add wasm32-unknown-unknown
# RUN cargo update -p parity-db
RUN cargo build --release

FROM debian:buster-slim AS runtime
WORKDIR /builds/dot-marketplace-v2
COPY --from=builder /builds/dot-marketplace-v2/target/release/dot_marketplace_node /usr/local/bin
EXPOSE 9944
CMD ["/usr/local/bin/dot_marketplace_node", "--dev", "--ws-external"]

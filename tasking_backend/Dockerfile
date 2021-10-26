FROM paritytech/ci-linux:production AS builder

RUN apt-get update \
    && apt-get install -y git

RUN git clone --single-branch -b Phase1_Milestone3 https://github.com/WowLabz/tasking_backend.git

WORKDIR /builds/tasking_backend/
RUN cargo update -p parity-db
RUN cargo build --release

FROM debian:buster-slim AS runtime
WORKDIR /builds/tasking_backend
COPY --from=builder /builds/tasking_backend/target/release/node-template /usr/local/bin
EXPOSE 9944
CMD ["/usr/local/bin/node-template", "--dev", "--ws-external"]
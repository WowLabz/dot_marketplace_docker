FROM paritytech/ci-linux:production

RUN apt-get update \
    && apt-get install -y git

RUN git clone --single-branch -b Phase1_Milestone1 https://github.com/WowLabz/tasking_backend.git


RUN echo "hello"
RUN pwd
RUN ls -la

WORKDIR /builds/tasking_backend/
RUN echo "bye"
RUN pwd
RUN ls -la

EXPOSE 9944

RUN cargo build --release
RUN echo "later"
RUN pwd
RUN ls -la
CMD ["./target/release/node-template", "--dev", "--ws-external"]
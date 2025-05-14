FROM rust:latest as cargo-build

WORKDIR /usr/src/

COPY . .

RUN cargo build --release

# ------------------------------------------------------------------------------
# Package Stage
# ------------------------------------------------------------------------------

FROM ubuntu:jammy

# create user to limit access in container
RUN groupadd -g 1001 json_rpc_snoop && useradd -r -u 1001 -g json_rpc_snoop json_rpc_snoop
RUN apt-get update && apt-get install -y libssl3 ca-certificates && rm -rf /var/lib/apt/lists/*
WORKDIR /home/json_rpc_snoop/bin/

COPY --from=cargo-build /usr/src/target/release/json_rpc_snoop .

RUN chown -R json_rpc_snoop:json_rpc_snoop /home/json_rpc_snoop/

USER json_rpc_snoop

ENTRYPOINT ["/home/json_rpc_snoop/bin/json_rpc_snoop"]

CMD ["--help"]
FROM --platform=linux/amd64 ubuntu:22.04 as builder

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y build-essential clang

COPY . /repo
WORKDIR /repo
RUN make -j8
RUN clang++ /repo/mayhem/fuzz_u8decode.cpp -fsanitize=fuzzer,address -I /repo/ -o /fuzz

FROM ubuntu:22.04 as package
COPY --from=builder /repo/msort /
COPY --from=builder /fuzz /fuzz_u8decode

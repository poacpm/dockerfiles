FROM ubuntu:19.04

RUN apt-get update \
 && apt-get install -y git cmake libboost-all-dev libssl-dev clang pkg-config

RUN git clone -q -b v3.0.0 https://github.com/ToruNiina/toml11.git
 && cd toml11
 && mkdir build
 && cd build
 && cmake -Dtoml11_BUILD_TEST=OFF ..
 && make
 && make install
 && cd ../../
 && rm -rf toml11

ENV CXX clang++

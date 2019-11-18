FROM ubuntu:19.10

RUN apt-get -qq update \
 && apt-get install -y -qq git cmake libboost-all-dev libssl-dev libgit2-dev clang-7 pkg-config

RUN git clone -q -b v3.1.0 https://github.com/ToruNiina/toml11.git \
 && cd toml11 \
 && mkdir build \
 && cd build \
 && cmake -Dtoml11_BUILD_TEST=OFF .. \
 && make \
 && make install \
 && cd ../../ \
 && rm -rf toml11

ENV CXX clang++-7

FROM ubuntu:19.04

RUN apt-get -qq update \
 && apt-get install -y -qq file pkg-config git cmake libboost-all-dev libssl-dev libgit2-dev clang-6.0

ENV CC clang-6.0
ENV CXX clang++-6.0

RUN git clone -q -b v3.4.0 https://github.com/ToruNiina/toml11.git \
 && cd toml11 \
 && mkdir build \
 && cd build \
 && cmake -DCMAKE_BUILD_TYPE=Release -Dtoml11_BUILD_TEST=OFF .. \
 && make install \
 && cd ../../ \
 && rm -rf toml11

FROM ubuntu:19.04

RUN apt-get update \
 && apt-get install -y git cmake g++-9-powerpc-linux-gnu file pkg-config \
 && ln -sf /usr/bin/powerpc-linux-gnu-g++-9 /usr/bin/g++ \
 && ln -sf /usr/bin/powerpc-linux-gnu-gcc-9 /usr/bin/powerpc-linux-gnu-gcc

RUN git clone -q -b OpenSSL_1_1_1b https://github.com/openssl/openssl.git \
 && cd openssl \
 && ./Configure linux-ppc -static --cross-compile-prefix=powerpc-linux-gnu- \
 && make \
 && make install \
 && cd ../ \
 && rm -rf openssl

RUN git clone -q -b boost-1.70.0 --recursive https://github.com/boostorg/boost.git \
 && cd boost \
 && ./bootstrap.sh \
 && ./b2 link=static install -j2 \
 && cd ../ \
 && rm -rf boost

ENV CXX powerpc-linux-gnu-g++-9

RUN git clone -q -b v3.0.0 https://github.com/ToruNiina/toml11.git
 && cd toml11
 && mkdir build
 && cd build
 && cmake -Dtoml11_BUILD_TEST=OFF ..
 && make
 && make install
 && cd ../../
 && rm -rf toml11

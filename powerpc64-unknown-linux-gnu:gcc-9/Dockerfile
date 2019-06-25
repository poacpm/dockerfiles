FROM ubuntu:19.04

RUN apt-get update \
 && apt-get install -y git cmake g++-9-powerpc64-linux-gnu file pkg-config \
 && ln -s /usr/bin/powerpc64-linux-gnu-g++-9 /usr/bin/g++ \
 && ln -s /usr/bin/powerpc64-linux-gnu-gcc-9 /usr/bin/powerpc64-linux-gnu-gcc

RUN git clone -q -b OpenSSL_1_1_1b https://github.com/openssl/openssl.git \
 && cd openssl \
 && ./Configure linux-ppc64 -static --cross-compile-prefix=powerpc64-linux-gnu- \
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

ENV CXX powerpc64-linux-gnu-g++-9

RUN git clone -q -b yaml-cpp-0.6.2 https://github.com/jbeder/yaml-cpp.git \
 && cd yaml-cpp \
 && mkdir build \
 && cd build \
 && cmake -DYAML_CPP_BUILD_TESTS=OFF .. \
 && make \
 && make install \
 && cd ../../ \
 && rm -rf yaml-cpp

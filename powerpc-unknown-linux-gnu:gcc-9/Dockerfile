FROM ubuntu:19.04

RUN apt-get update \
 && apt-get install -y git cmake g++-9-powerpc-linux-gnu \
 && ln -s /usr/bin/powerpc-linux-gnu-g++-9 /usr/bin/g++ \
 && ln -s /usr/bin/powerpc-linux-gnu-gcc-9 /usr/bin/powerpc-linux-gnu-gcc

RUN git clone -q -b OpenSSL_1_1_1b https://github.com/openssl/openssl.git \
 && cd openssl \
 && ./Configure linux-ppc --shared -fPIC --prefix=/usr/local/ --cross-compile-prefix=powerpc-linux-gnu- \
 && make \
 && make install \
 && cd ../ \
 && rm -rf openssl

RUN git clone -q -b boost-1.67.0 --recursive https://github.com/boostorg/boost.git \
 && cd boost \
 && ./bootstrap.sh \
 && ./b2 link=static install -j2 \
 && cd ../ \
 && rm -rf boost

ENV CXX powerpc-linux-gnu-g++-9

RUN git clone -q -b yaml-cpp-0.6.2 https://github.com/jbeder/yaml-cpp.git \
 && cd yaml-cpp \
 && mkdir build \
 && cd build \
 && cmake -DYAML_CPP_BUILD_TESTS=OFF .. \
 && make \
 && make install \
 && cd ../../ \
 && rm -rf yaml-cpp
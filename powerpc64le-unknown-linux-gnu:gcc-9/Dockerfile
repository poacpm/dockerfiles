FROM ubuntu:19.10

RUN apt-get -qq update \
 && apt-get install -y -qq git cmake g++-9-powerpc64le-linux-gnu file pkg-config \
 && ln -sf /usr/bin/powerpc64le-linux-gnu-gcc-9 /usr/bin/powerpc64le-linux-gnu-gcc

RUN git clone -q -b OpenSSL_1_1_1b https://github.com/openssl/openssl.git \
 && cd openssl \
 && ./Configure linux-ppc64le -static --cross-compile-prefix=powerpc64le-linux-gnu- \
 && make \
 && make install \
 && cd ../ \
 && rm -rf openssl

RUN git clone -q -b boost-1.71.0 --recursive https://github.com/boostorg/boost.git \
 && cd boost \
 && apt-get update && apt-get install -y g++-9 && ln -sf /usr/bin/g++-9 /usr/bin/g++ \
 && ./bootstrap.sh \
 && rm -rf /usr/bin/g++ && ln -sf /usr/bin/powerpc64le-linux-gnu-g++-9 /usr/bin/g++ \
 && ./b2 link=static install -j2 \
 && cd ../ \
 && rm -rf boost

ENV CXX powerpc64le-linux-gnu-g++-9
ENV CC powerpc64le-linux-gnu-gcc

RUN git clone -q -b v3.1.0 https://github.com/ToruNiina/toml11.git \
 && cd toml11 \
 && mkdir build \
 && cd build \
 && cmake -DCMAKE_BUILD_TYPE=Release -Dtoml11_BUILD_TEST=OFF .. \
 && make \
 && make install \
 && cd ../../ \
 && rm -rf toml11

RUN git clone -q -b v0.28.2 https://github.com/libgit2/libgit2.git \
 && cd libgit2 \
 && mkdir build \
 && cd build \
 && cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=OFF -DBUILD_CLAR=OFF .. \
 && make \
 && make install \
 && cd ../../ \
 && rm -rf libgit2


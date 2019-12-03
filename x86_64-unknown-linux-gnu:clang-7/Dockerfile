FROM ubuntu:19.10

RUN apt-get -qq update \
 && apt-get install -y -qq git cmake clang-7 file pkg-config

ENV CC clang-7
ENV CXX clang++-7

RUN git clone -q -b OpenSSL_1_1_1b https://github.com/openssl/openssl.git \
 && cd openssl \
 && ./config no-shared \
 && make \
 && make install \
 && cd ../ \
 && rm -rf openssl

RUN git clone -q -b boost-1.71.0 --recursive https://github.com/boostorg/boost.git \
 && cd boost \
 && ./bootstrap.sh \
 && ./b2 link=static install -j2 || exit 0 \
 && cd ../ \
 && rm -rf boost

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

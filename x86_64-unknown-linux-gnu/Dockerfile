FROM linuxbrew/linuxbrew

RUN brew update \
 && brew install \
 curl \
 cmake \
 boost \
 gcc@7 \
 gcc@8 \
 llvm

USER root

RUN ln -s /home/linuxbrew/.linuxbrew/include/boost /usr/local/include/boost \
 && find /home/linuxbrew/.linuxbrew/lib/libboost_* \
  | awk -F/ '{print $NF}' \
  | xargs -I{} ln -s /home/linuxbrew/.linuxbrew/lib/{} /usr/local/lib/{} \
 && find /home/linuxbrew/.linuxbrew/lib/libcurl* \
  | awk -F/ '{print $NF}' \
  | xargs -I{} ln -s /home/linuxbrew/.linuxbrew/lib/{} /usr/local/lib/{} \
 && find /home/linuxbrew/.linuxbrew/lib/libgmp* \
  | awk -F/ '{print $NF}' \
  | xargs -I{} ln -s /home/linuxbrew/.linuxbrew/lib/{} /usr/local/lib/{}

ENV CXX g++-8

# Install yaml-cpp
RUN git clone -q https://github.com/jbeder/yaml-cpp.git \
 && mkdir yaml-cpp/build \
 && cd yaml-cpp/build \
 && cmake .. \
 && make \
 && make install \
 && cd ../../ \
 && rm -rf yaml-cpp

# Install CVC4
RUN apt-get update -qq \
 && apt-get install -y -qq openjdk-8-jdk m4 \
 && git clone -q https://github.com/cvc4/cvc4 \
 && cd cvc4/ \
 && ./contrib/get-antlr-3.4 \
 && ./contrib/get-symfpu \
 && ./contrib/get-gmp \
 && cp ./gmp-6.1.2/lib/* /usr/local/lib/ \
 && cp -r ./gmp-6.1.2/include/* /usr/local/include/ \
 && sed -i -e 's/cmake_opts=""/cmake_opts="-DCMAKE_BUILD_WITH_INSTALL_RPATH=1"/' configure.sh \
 && ./configure.sh --static --symfpu \
 && cd build \
 && make -j2 \
 && make check \
 && make install \
 && mkdir /usr/local/include/cvc4 \
 && mv /usr/local/include/api \
       /usr/local/include/base \
       /usr/local/include/context \
       /usr/local/include/cvc4.h \
       /usr/local/include/cvc4_public.h \
       /usr/local/include/cvc4parser_public.h \
       /usr/local/include/expr \
       /usr/local/include/options \
       /usr/local/include/parser \
       /usr/local/include/printer \
       /usr/local/include/proof \
       /usr/local/include/smt \
       /usr/local/include/smt_util \
       /usr/local/include/theory \
       /usr/local/include/util \
       /usr/local/include/cvc4

#USER linuxbrew

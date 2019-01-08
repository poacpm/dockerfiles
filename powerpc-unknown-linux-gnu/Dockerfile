FROM japaric/powerpc-unknown-linux-gnu


RUN apt-get update -qq \
 && apt-get install -y -qq --no-install-recommends \
 ca-certificates \
 curl \
 file \
 g++ \
 git \
 locales \
 make \
 uuid-runtime \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && localedef -i en_US -f UTF-8 en_US.UTF-8 \
 && useradd -m -s /bin/bash linuxbrew \
 && echo 'linuxbrew ALL=(ALL) NOPASSWD:ALL' >>/etc/sudoers

USER linuxbrew
WORKDIR /home/linuxbrew
ENV PATH=/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:$PATH \
  SHELL=/bin/bash

RUN git clone -q https://github.com/Linuxbrew/brew.git /home/linuxbrew/.linuxbrew/Homebrew \
 && mkdir /home/linuxbrew/.linuxbrew/bin \
 && ln -s ../Homebrew/bin/brew /home/linuxbrew/.linuxbrew/bin/ \
 && brew config


RUN brew update \
 && brew install \
 curl \
 cmake \
 yaml-cpp \
 boost

USER root

RUN ln -s /home/linuxbrew/.linuxbrew/include/boost /usr/local/include/boost \
 && find /home/linuxbrew/.linuxbrew/lib/libboost_* \
  | awk -F/ '{print $NF}' \
  | xargs -I{} ln -s /home/linuxbrew/.linuxbrew/lib/{} /usr/local/lib/{} \
 && find /home/linuxbrew/.linuxbrew/lib/libcurl* \
  | awk -F/ '{print $NF}' \
  | xargs -I{} ln -s /home/linuxbrew/.linuxbrew/lib/{} /usr/local/lib/{}


# Install yaml-cpp
RUN git clone -q https://github.com/jbeder/yaml-cpp.git \
 && mkdir yaml-cpp/build \
 && cd yaml-cpp/build \
 && cmake .. \
 && make \
 && make install \
 && cd ../../ \
 && rm -rf yaml-cpp

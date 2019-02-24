FROM linuxbrew/linuxbrew

RUN brew update \
 && brew install \
 cmake \
 boost \
 gcc@7 \
 gcc@8

USER root

RUN ln -s /home/linuxbrew/.linuxbrew/include/boost /usr/local/include/boost \
 && find /home/linuxbrew/.linuxbrew/lib/libboost_* \
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

#USER linuxbrew

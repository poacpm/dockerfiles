FROM linuxbrew/linuxbrew

RUN brew update \
 && brew install \
 cmake \
 boost \
 yaml-cpp \
 gcc@7 \
 gcc@8 \
 gcc@9

USER root

RUN ln -s /home/linuxbrew/.linuxbrew/include/boost /usr/local/include/boost \
 && find /home/linuxbrew/.linuxbrew/lib/libboost_* \
  | awk -F/ '{print $NF}' \
  | xargs -I{} ln -s /home/linuxbrew/.linuxbrew/lib/{} /usr/local/lib/{}

ENV CXX g++-9

# Install yaml-cpp
#RUN git clone -q https://github.com/jbeder/yaml-cpp.git -b yaml-cpp-0.6.2 \
# && mkdir yaml-cpp/build \
# && cd yaml-cpp/build \
# && cmake -DYAML_CPP_BUILD_TESTS=OFF .. \
# && make \
# && make install \
# && cd ../../ \
# && rm -rf yaml-cpp

#USER linuxbrew

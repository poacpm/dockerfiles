FROM poacpm/x86_64-unknown-linux-gnu

RUN git clone -q https://github.com/poacpm/poac.git \
 && cd poac \
 && mkdir build \
 && cd build \
 && cmake .. \
 && make \
 && make install \
 && cd ../../ \
 && rm -rf poac

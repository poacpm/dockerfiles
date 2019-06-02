FROM poacpm/x86_64-unknown-linux-gnu

RUN git clone -q https://github.com/poacpm/poac.git -b 0.2.1 \
 && cd poac \
 && mkdir build \
 && cd build \
 && cmake .. \
 && make \
 && make install \
 && cd ../../ \
 && rm -rf poac

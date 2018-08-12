# Matches raspian version
FROM debian:9.4

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    ca-certificates \
    cmake \
    gcc \
    libc6-dev \
    make \
    pkg-config

COPY xargo.sh /
RUN bash /xargo.sh

# Do we need to build a custom OpenSSH?
# COPY openssl.sh qemu.sh /
RUN apt-get install -y --no-install-recommends \
    g++-arm-linux-gnueabihf \
    libc6-dev-armhf-cross
    #libc6-dev-armhf-cross && \
    # bash /openssl.sh linux-armv4 arm-linux-gnueabihf- && \
    # bash /qemu.sh arm

RUN dpkg --add-architecture armhf && \
    apt-get update && \
    apt-get install -y libgl-dev:armhf xserver-xorg-dev:armhf libssl-dev:armhf \
    libxrandr-dev:armhf libxinerama-dev:armhf libxcursor-dev:armhf libxi-dev:armhf

ENV CARGO_TARGET_ARMV7_UNKNOWN_LINUX_GNUEABIHF_LINKER=arm-linux-gnueabihf-gcc \
    CARGO_TARGET_ARMV7_UNKNOWN_LINUX_GNUEABIHF_RUNNER=qemu-arm \
    CC_armv7_unknown_linux_gnueabihf=arm-linux-gnueabihf-gcc \
    CXX_armv7_unknown_linux_gnueabihf=arm-linux-gnueabihf-g++ \
    OPENSSL_DIR=/usr/lib/arm-linux-gnueabihf \
    OPENSSL_INCLUDE_DIR=/usr/include/arm-linux-gnueabihf/openssl \
    OPENSSL_LIB_DIR=/usr/lib/arm-linux-gnueabihf \
    QEMU_LD_PREFIX=/usr/arm-linux-gnueabihf \
    RUST_TEST_THREADS=1

ARG UBUNTU_RELEASE=24.10

# Build the chiselled filesystem based on the desired slices.
FROM ubuntu:$UBUNTU_RELEASE AS base
ARG UBUNTU_RELEASE
ARG TARGETARCH

# Get chisel binary
ADD https://github.com/canonical/chisel/releases/download/v0.10.0/chisel_v0.10.0_linux_$TARGETARCH.tar.gz chisel.tar.gz
RUN tar -xvf chisel.tar.gz -C /usr/bin/
RUN apt-get update \
   && DEBIAN_FRONTEND=noninteractive apt-get install -y ca-certificates
WORKDIR /rootfs
RUN chisel cut --release ubuntu-$UBUNTU_RELEASE --root /rootfs \
   base-files_base \
   base-files_release-info \
   ca-certificates_data \
   libgcc-s1_libs \
   zlib1g_libs \
   libc6_libs

FROM scratch

ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

COPY --from=base /rootfs /
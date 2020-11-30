FROM postgres:9.6

RUN apt-get update  \
 && apt-get install --yes \
        nasm \
        build-essential \
        ocaml \
        automake \
        autoconf \
        git \
        libtool \
        wget \
        python \
        #Have to use downgraded openSSL headers due to compilation errors.
        libssl1.0-dev \
        libcurl4-openssl-dev \
        protobuf-compiler \
        libprotobuf-dev \
        postgresql-server-dev-all \
 && rm -rf /var/lib/apt/lists/*

COPY docker/sgx-deps.mk /opt/Makefile
WORKDIR /opt
RUN make

RUN ln -s /opt/intel/sgxsdk/lib64/libsgx_urts.so /lib/libsgx_urts.so && ln -s /opt/intel/sgxsdk/lib64/libsgx_uae_service.so /lib/libsgx_uae_service.so

COPY . /home/stealthDB

WORKDIR /home/stealthDB
RUN make && make install

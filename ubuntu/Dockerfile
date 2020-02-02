
FROM ubuntu
ENV DEBIAN_FRONTEND=nonintercative
RUN apt-get update && apt-get install -y build-essential uuid-dev git python3.8. python3-pip

# install mono
RUN apt install gnupg ca-certificates
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
RUN echo "deb https://download.mono-project.com/repo/ubuntu stable-bionic main" | tee /etc/apt/sources.list.d/mono-official-stable.list
RUN apt-get update && apt-get install --yes mono-devel
RUN pip3 install --upgrade edk2-pytool-extensions

# Setup Omnicache for dev work
ENV OMNICACHE_PATH=/opt/src/omnicache
RUN echo 'alias gcl="git clone --reference ${OMNICACHE_PATH}"' >> ~/.bashrc
RUN omnicache -a edk2_upstream https://github.com/tianocore/edk2 -a openssl https://github.com/openssl/openssl.git true -a softfloat https://github.com/ucb-bar/berkeley-softfloat-3.git --init ${OMNICACHE_PATH}
RUN omnicache -a softfloat https://github.com/ucb-bar/berkeley-softfloat-3.git -a cmocka https://git.cryptomilk.org/projects/cmocka.git --init ${OMNICACHE_PATH}

# make a workspace
RUN mkdir -p /opt/src/ && \
    cd /opt/src
RUN echo "#!/bin/bash\necho \"WELCOME TO Project Mu Linux Build and Test container for UEFI!!\n\
   The suggested process is as follows: \n\
   1. Make a base directory here for your work\n\
   2. Checkout out your code.  use 'gcl <url>' for best results\n\
   3. Create a virtual environment.  'python3.8 -m venv <virtual env name>'\n\
   4. Activate it 'source <venv name>/bin/activate' \n\
   5. install your pip requirements \n\
   6. Get going with Stuart \n\"" > /entrypoint.sh



#   git clone --reference ${OMNICACHE_PATH} https://github.com/tianocore/edk2
#   cd edk2 && \
#   make -C BaseTools
#ADD entrypoint.sh /
RUN chmod +x /entrypoint.sh

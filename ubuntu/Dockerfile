
FROM ubuntu

ENV DEBIAN_FRONTEND=nonintercative

# key for mono
RUN apt -y update && apt install -y --no-install-recommends gnupg ca-certificates && apt autoremove && apt clean
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
RUN echo "deb https://download.mono-project.com/repo/ubuntu stable-bionic main" | tee /etc/apt/sources.list.d/mono-official-stable.list

RUN apt-get update && apt-get install --no-install-recommends -y build-essential uuid-dev git python3.8. python3-pip install mono-devel && \
    apt autoremove && apt clean

RUN pip3 install --upgrade edk2-pytool-extensions

# Setup Omnicache for dev work
ENV OMNICACHE_PATH=/opt/src/omnicache
RUN echo 'alias gcl="git clone --reference ${OMNICACHE_PATH}"' >> ~/.bashrc
RUN omnicache -a edk2_upstream https://github.com/tianocore/edk2 -a openssl https://github.com/openssl/openssl.git true \
    -a softfloat https://github.com/ucb-bar/berkeley-softfloat-3.git -a cmocka https://git.cryptomilk.org/projects/cmocka.git --init ${OMNICACHE_PATH}

# WELCOME TO Project Mu Linux Build and Test container for UEFI!!
#   The suggested process is as follows:
#   1. Make a base directory for your work
#   2. Checkout out your code.  use 'gcl <url>' for best results
#   3. Create a virtual environment.  'python3.8 -m venv <virtual env name>'
#   4. Activate it 'source <venv name>/bin/activate'
#   5. install your pip requirements
#   6. Get going with Stuart
#      a. stuart_setup -c .pytool/CISettings.py TOOL_CHAIN_TAG=GCC5 -a X64
#      b. stuart_update -c .pytool/CISettings.py TOOL_CHAIN_TAG=GCC5 -a X64
#      c. build base tools BaseTools/Edk2BaseToolsBuild.py
#      d. stuart_ci_build -c .pytool/CISettings.py TOOL_CHAIN_TAG=GCC5 -a X64

ENTRYPOINT ["/bin/bash"]
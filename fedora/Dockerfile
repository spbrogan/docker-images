
FROM fedora:31

# Add mono server
RUN rpm --import "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF" && \
    su -c 'curl https://download.mono-project.com/repo/centos8-stable.repo | tee /etc/yum.repos.d/mono-centos8-stable.repo'

# install tools
RUN dnf -y update && \
    dnf -y groupinstall development-tools && \ 
    dnf -y install git gcc gcc-c++ python3.8 python3-pip libuuid-devel mono-devel && \
    dnf clean all

# install Pytools
RUN pip3 install --upgrade edk2-pytool-extensions

# Setup Omnicache for dev work
ENV OMNICACHE_PATH=/opt/src/omnicache
RUN echo 'alias gcl="git clone --reference ${OMNICACHE_PATH}"' >> ~/.bashrc
RUN omnicache -a edk2_upstream https://github.com/tianocore/edk2 -a openssl https://github.com/openssl/openssl.git true -a softfloat https://github.com/ucb-bar/berkeley-softfloat-3.git --init ${OMNICACHE_PATH} && \
    omnicache -a cmocka https://git.cryptomilk.org/projects/cmocka.git --init ${OMNICACHE_PATH}


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





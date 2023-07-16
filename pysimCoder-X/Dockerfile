FROM debian:bookworm

RUN apt-get -y update
RUN apt-get -y dist-upgrade

RUN apt-get -y install \
    gcc \
    gfortran \
    git \
    locate \
    less \
    net-tools \
    xfce4-terminal \
    make \
    python3-pip \
    kconfig-frontends \
    cmake \
    binutils \
    emacs \
    x11vnc \
    python3 \
    python3-numpy \
    python3-scipy \
    python3-sympy \
    python3-matplotlib \
    python3-pip \
    jupyter-qtconsole \
    python3-lxml \
    python3-pyqtgraph \
    libopenblas-dev \
    liblapack-dev \
    libxml2-dev \
    libcomedi-dev \
    python3-pyqt5 \
    nano \
    thunar \
    gedit
    
RUN apt-get -y install \
    qtbase5-dev \
    qt5-qmake \
    libqt5webkit5-dev \
    libqt5serialport5-dev \
    libqt5websockets5-dev \
    libqt5svg5-dev \
    liblua5.4-dev \
    doctest-dev

RUN apt-get -y clean
RUN apt-get -y autoremove

WORKDIR .
RUN git clone https://github.com/robertobucher/pysimCoder

COPY make4docker.mak  ./pysimCoder
WORKDIR ./pysimCoder
RUN make -f make4docker.mak

WORKDIR /
RUN mkdir SHV
WORKDIR SHV
RUN git clone https://github.com/silicon-heaven/shvapp
RUN git clone https://github.com/silicon-heaven/shvspy

WORKDIR shvapp
RUN git submodule update --init --recursive
RUN mkdir build
WORKDIR build
RUN cmake -DCMAKE_INSTALL_PREFIX=..  -DUSE_QT6=OFF ..
RUN make
RUN make install

WORKDIR /SHV/shvspy
RUN mkdir -p /root/.config/Elektroline
COPY shvspy.conf /root/.config/Elektroline/
RUN git submodule update --init --recursive
RUN mkdir build
WORKDIR build
RUN cmake -DCMAKE_INSTALL_PREFIX=.. -DUSE_QT6=OFF ..
RUN make
RUN make install

WORKDIR /pysimCoder/CodeGen/LinuxRT/devices
RUN make SHV=1 PYSUPSICTRL=/pysimCoder
    
COPY shv /usr/local/bin

# install NuttX tools:
RUN apt-get -y install \
    tio \
    minicom \
    kconfig-frontends \
    openocd  \
    binutils-arm-none-eabi \
    gcc-arm-none-eabi
WORKDIR /
RUN git clone https://github.com/apache/nuttx.git NUTTX/nuttx
RUN git clone https://github.com/apache/nuttx-apps NUTTX/apps

RUN printf "alias ls='ls --color=auto'\n" >> /root/.bashrc

WORKDIR /
RUN mkdir psc

WORKDIR /psc
CMD ["xfce4-terminal"]
#sudo docker run --rm --env="DISPLAY" --net=host -v $XAUTHORITY:/tmp/.XAuthority -e XAUTHORITY=/tmp/.XAuthority --privileged rcp-dev


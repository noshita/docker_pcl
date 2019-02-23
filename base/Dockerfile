FROM ubuntu:bionic
LABEL maintainer="noshita"

# ENV
ENV DEBIAN_FRONTEND=noninteractive

# Requred packages
RUN apt-get update && apt-get install -y \
	aptitude \
	cifs-utils \
	emacs \
	tmux \
	htop \
	git \
	iputils-ping \
	net-tools \
	build-essential \
	linux-libc-dev \
	libncurses5-dev \
	cmake \
	libboost-all-dev \
	libeigen3-dev \
	libflann-dev \
	libglew-dev \
	libgtest-dev \
	libqhull-dev \
	libqt5opengl5-dev \
	libusb-dev \
	libvtk7-dev \
	libvtk7-qt-dev \
	qtbase5-dev

# PCL
RUN mkdir ./working_dir && cd ./working_dir
WORKDIR ./working_dir
RUN	git clone https://github.com/PointCloudLibrary/pcl.git && \
	cd ./pcl && \
	mkdir ./build && cd ./build && \
	cmake -DCMAKE_CXX_FLAGS='-Wall -Wextra -Wabi -O2' \
            -DBUILD_simulation=ON \
            -DBUILD_surface_on_nurbs=ON \
            -DBUILD_examples=ON \
            -DBUILD_tools=ON \
            -DBUILD_apps=ON \
            -DBUILD_apps_3d_rec_framework=ON \
            -DBUILD_apps_cloud_composer=ON \
            -DBUILD_apps_in_hand_scanner=ON \
            -DBUILD_apps_modeler=ON \
            -DBUILD_apps_point_cloud_editor=ON \
            .. && \
    make -j ${THREADS:-`cat /proc/cpuinfo | grep processor | wc -l`} &&\
    make install

RUN apt-get install -y \
	ubuntu-desktop

# NAS
RUN mkdir /mnt/nas

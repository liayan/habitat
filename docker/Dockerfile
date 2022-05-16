FROM nvidia/cuda:11.6.2-cudnn8-devel-ubuntu20.04
MAINTAINER Liang Yan <liayan@mtu.edu>

#RUN rm /etc/apt/sources.list.d/cuda.list
#RUN rm /etc/apt/sources.list.d/nvidia-ml.list
#RUN apt-key del 7fa2af80
#RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/3bf863cc.pub
#RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/7fa2af80.pub

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update --fix-missing && \ 
  apt-get install --no-install-recommends -y software-properties-common && \
  apt-get install --no-install-recommends -y sudo vim cmake&& \
  apt-get install --no-install-recommends -y python3-pip python3-setuptools python3-dev && \
  apt-get install --no-install-recommends -y wget bzip2 ca-certificates libssl-dev && \
  rm -rf /var/lib/apt/lists/*

RUN pip3 install wheel && pip3 install numpy PyYAML
Run pip3 install torch==1.11.0+cu115 torchvision==0.12.0+cu115  -f https://download.pytorch.org/whl/cu115/torch_stable.html
RUN pip3 install \
  pillow \
  pandas \
  tqdm

# Download cmake
RUN wget "https://github.com/Kitware/CMake/releases/download/v3.21.0/cmake-3.21.0.tar.gz" -O /opt/cmake-3.21.0.tar.gz && \
  cd /opt && tar xzf cmake-3.21.0.tar.gz

# Install cmake
RUN cd /opt/cmake-3.21.0 && \
  ./bootstrap && \
  make -j 16 && \
  make install


# NOTE: gosu is used in create-user.sh
RUN mkdir ~/.gnupg && echo "disable-ipv6" >> ~/.gnupg/dirmngr.conf
#RUN gpg --keyserver keyserver.ubuntu.com --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
#RUN wget "https://github.com/tianon/gosu/releases/download/1.11/gosu-$(dpkg --print-architecture | awk -F- '{ print $NF }')" -O /usr/local/bin/gosu && \
#  wget "https://github.com/tianon/gosu/releases/download/1.11/gosu-$(dpkg --print-architecture | awk -F- '{ print $NF }').asc" -O /usr/local/bin/gosu.asc && \
#  gpg --verify /usr/local/bin/gosu.asc && \
#  rm /usr/local/bin/gosu.asc && \
#  chmod +x /usr/local/bin/gosu

#COPY create-user.sh /usr/local/bin/create-user.sh
#RUN chmod +x /usr/local/bin/create-user.sh
#ENTRYPOINT ["/usr/local/bin/create-user.sh"]
CMD ["/bin/bash"]

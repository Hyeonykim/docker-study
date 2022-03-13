FROM ubuntu

LABEL maintainer="hyeonykim <walnbobbbol@gmail.com>"
LABEL description="ubuntu with default configuration"

#########################
# Envirunment Variables #
#########################
ARG srcAptPackageList="/config/apt/aptPackageList.dat"
ARG aptPackageList="/root/config/aptPackageList.dat"
# Enable non-interactive mode apt operation
ENV DEBIAN_FRONTEND=noninteractive
ARG APT_OPTS="-o Acquire::Check-Valid-Until=false \
				-o APT::Keep-Downloaded-Packages=true"

########################
# Install apt packages #
########################
ADD $srcAptPackageList $aptPackageList
RUN apt-get $APT_OPTS update
RUN cat $aptPackageList | tr '\n' ' ' | xargs apt-get $APT_OPTS -y install

WORKDIR /root

# The following command make the container keep alive
ENTRYPOINT ["tail", "-f", "/dev/null"]

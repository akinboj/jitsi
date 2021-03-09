# Ref for this build --> https://hub.docker.com/layers/jitsi/jicofo/stable-5390-3/images/sha256-cf0d686a0f0f88361ec94576480f2d35b973d24383527715f6da2c7812790885?context=explore
FROM fhirfactory/pegacorn-base-docker-jitsi:1.0.0

# Buildkit
RUN mkdir -p /usr/share/man/man1 \
	&& wget -q https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public -O /etc/apt/trusted.gpg.d/openjdk.asc \
	&& echo "deb https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/ buster main" > /etc/apt/sources.list.d/openjdk.list \
	&& apt-dpkg-wrap apt-get update \
	&& apt-dpkg-wrap apt-get install -y adoptopenjdk-8-hotspot-jre \
	&& apt-cleanup

# https://stackoverflow.com/questions/46247032/how-to-solve-invoke-rc-d-policy-rc-d-denied-execution-of-start-when-building
# Without this command, jicofo will not start		
RUN printf '#!/bin/sh\nexit 0' > /usr/sbin/policy-rc.d

RUN apt-dpkg-wrap apt-get update \ 
	&& apt-dpkg-wrap apt-get install -y jicofo \ 
	&& apt-cleanup

# Date-time build argument
ARG IMAGE_BUILD_TIMESTAMP
ENV IMAGE_BUILD_TIMESTAMP=${IMAGE_BUILD_TIMESTAMP}
RUN echo IMAGE_BUILD_TIMESTAMP=${IMAGE_BUILD_TIMESTAMP}

COPY rootfs/ /
VOLUME /config


# Run expressvpn in a container

FROM debian:bullseye-slim

LABEL maintainer="brocole@me.com"

ENV ACTIVATION_CODE code
ENV LOCATION smart
ENV PREFERRED_PROTOCOL auto
ENV LIGHTWAY_CIPHER auto

ARG APP=expressvpn_3.25.0.13-1_amd64.deb

RUN apt-get update && apt-get install -y --no-install-recommends \
    libterm-readkey-perl ca-certificates wget expect iproute2 curl procps libnm0 \
    && rm -rf /var/lib/apt/lists/* \
    && wget -q "https://www.expressvpn.works/clients/linux/${APP}" -O /tmp/${APP} \
    && dpkg -i /tmp/${APP} \
    && rm -rf /tmp/*.deb \
    && apt-get purge -y --auto-remove wget

COPY entrypoint.sh test/dockerfiles-master/entrypoint.sh
COPY expressvpnActivate.sh test/dockerfiles-master/expressvpn/expressvpnActivate.sh

ENTRYPOINT ["/bin/bash", "/test/dockerfiles-master/expressvpn/expressvpnentrypoint.sh"]

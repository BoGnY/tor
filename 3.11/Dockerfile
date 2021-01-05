FROM dockage/alpine:3.11-openrc

LABEL maintainer="me@bogny.dev" \
    org.label-schema.name="tor" \
    org.label-schema.vendor="BoGnY" \
    org.label-schema.description="Docker Tor proxy (http and shell) built on Alpine Linux" \
    org.label-schema.license="MIT"

# Update the package repository and install Tor
RUN apk --no-cache --update add tor

RUN rc-update add tor default

# Add custom Tor config
COPY ./config/tor/torrc /etc/tor/torrc
COPY ./config/tor/torsocks.conf /etc/tor/torsocks.conf

# Set the correct owner
RUN chown -R tor /etc/tor

EXPOSE 9050 9051

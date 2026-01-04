ARG BUILD_FROM=ghcr.io/home-assistant/base:3.19
FROM $BUILD_FROM

# Set shell to bash (already available in HA base images)
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Install Ruby and build dependencies
ARG RUBY_VERSION=3.3.0
RUN \
    apk update && \
    apk add --no-cache \
        ruby \
        ruby-dev \
        ruby-bigdecimal \
        ruby-bundler \
        build-base \
        sqlite \
        sqlite-dev \
        curl \
        git \
        libc6-compat \
        libffi-dev \
        yaml-dev \
        zlib-dev \
        nodejs \
        npm \
        avahi-dev \
        avahi-compat-libdns_sd \
        avahi \
        dbus && \
    gem install bundler

# Create app directory
WORKDIR /app

# Copy Gemfile and install dependencies
COPY homechat/Gemfile homechat/Gemfile.lock ./
RUN bundle config set --local without 'development test' && \
    bundle config set --local deployment true && \
    bundle install

# Copy application code
COPY homechat/ ./

# Set production environment
ENV RAILS_ENV=production

# Build Tailwind CSS and precompile assets
RUN SECRET_KEY_BASE=dummy bundle exec rails tailwindcss:build
RUN SECRET_KEY_BASE=dummy bundle exec rails assets:precompile

# Copy root filesystem
COPY addon/homechat/rootfs /

# Create data directory for SQLite database and setup Avahi/D-Bus
RUN mkdir -p /data && chown nobody:nogroup /data && \
    mkdir -p /var/run/avahi-daemon && \
    mkdir -p /var/run/dbus && \
    mkdir -p /var/lib/dbus && \
    chmod 755 /var/run/avahi-daemon /var/run/dbus /var/lib/dbus

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="HomeChat Team" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="HomeChat Team" \
    org.opencontainers.image.authors="HomeChat Team" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/kebabmane/homechat-addon" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}

# Expose default port
EXPOSE 3000

# Set up s6-overlay entrypoint
ENTRYPOINT ["/init"]
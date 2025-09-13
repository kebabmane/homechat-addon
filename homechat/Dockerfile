ARG BUILD_FROM
FROM $BUILD_FROM

# Set shell to bash (already available in HA base images)
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Install Ruby and build dependencies
ARG RUBY_VERSION=3.3.0
RUN \
    apk add --no-cache \
        ruby \
        ruby-dev \
        ruby-bundler \
        build-base \
        sqlite \
        sqlite-dev \
        curl \
        git \
        libc6-compat \
        vips-dev \
        yaml-dev \
        zlib-dev && \
    gem install bundler

# Create app directory
WORKDIR /app

# Copy source code from the homechat directory
COPY homechat/Gemfile homechat/Gemfile.lock ./
RUN bundle config --global frozen 1
RUN bundle install --without development test

# Copy application code
COPY homechat/ ./

# Precompile assets for production
ENV RAILS_ENV=production
RUN SECRET_KEY_BASE_DUMMY=1 ./bin/rails assets:precompile

# Create non-root user
RUN addgroup -g 1000 -S rails && \
    adduser -u 1000 -D -S -G rails rails && \
    chown -R rails:rails /app

# Copy root filesystem first (as root for proper permissions)
COPY rootfs /

# Switch to rails user
USER rails:rails

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
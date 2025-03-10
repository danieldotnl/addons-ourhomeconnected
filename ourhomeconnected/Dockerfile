# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Copy uv from its official image
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# Install package from PyPI
ARG PACKAGE_VERSION=latest
RUN \
    if [ "${PACKAGE_VERSION}" = "latest" ]; then \
    uv pip install --system ohc-backend; \
    else \
    uv pip install --system ohc-backend==${PACKAGE_VERSION}; \
    fi

# Copy root filesystem
COPY rootfs /

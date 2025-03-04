# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Install Python and pip
RUN apk add --no-cache python3 py3-pip

# Download and install the wheel file
ARG WHEEL_VERSION
RUN \
    curl -sSLf -o /tmp/ohc_backend-${WHEEL_VERSION}-py3-none-any.whl \
    "https://github.com/danieldotnl/ohc-addon-backend/releases/download/v${WHEEL_VERSION}/ohc_backend-${WHEEL_VERSION}-py3-none-any.whl" && \
    pip3 install /tmp/ohc_backend-${WHEEL_VERSION}-py3-none-any.whl && \
    rm /tmp/ohc_backend-${WHEEL_VERSION}-py3-none-any.whl

# Copy root filesystem
COPY rootfs /

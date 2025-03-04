# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Check Python version and install if needed
RUN python3 --version || apk add --no-cache python3

# Copy uv from its official image
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# Download and install the wheel file
ARG WHEEL_VERSION
RUN \
    curl -sSLf -o /tmp/ohc_backend-${WHEEL_VERSION}-py3-none-any.whl \
    "https://github.com/danieldotnl/ohc-addon-backend/releases/download/v${WHEEL_VERSION}/ohc_backend-${WHEEL_VERSION}-py3-none-any.whl" && \
    uv venv --python 3.13 %% \
    uv pip install /tmp/ohc_backend-${WHEEL_VERSION}-py3-none-any.whl && \
    rm /tmp/ohc_backend-${WHEEL_VERSION}-py3-none-any.whl

# Copy root filesystem
COPY rootfs /

FROM android-tools:latest

ARG BUILD_TOOLS_VERSION
ARG PLATFORM_API_LEVEL

# Update AndroidSDK
# Get ids from sdkmanager --list
RUN yes 'y' | sdkmanager --licenses >/dev/null \
    && yes 'y' | sdkmanager "build-tools;${BUILD_TOOLS_VERSION}" \
    "platforms;android-${PLATFORM_API_LEVEL}" >/dev/null

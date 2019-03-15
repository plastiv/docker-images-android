FROM android-sdk:latest

ARG EMULATOR_API_LEVEL=28
ARG EMULATOR_VARIANT=google_apis
ARG EMULATOR_ARCH=x86_64

# Update AndroidSDK
# Get ids from sdkmanager --list
RUN yes 'y' | sdkmanager --licenses >/dev/null \
    && yes 'y' | sdkmanager "system-images;android-${EMULATOR_API_LEVEL};${EMULATOR_VARIANT};${EMULATOR_ARCH}" >/dev/null

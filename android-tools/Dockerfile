FROM debian:stretch

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

# Download java and android (emulator) dependencies
# to debug missing lib issues use ldconfig -p | grep libGL
# Dev deps are taken from https://developer.android.com/studio/install#linux
# https://issuetracker.google.com/issues/37094469
RUN DEBIAN_FRONTEND=noninteractive \
    && apt-get -qq update \
    && apt-get -qq install --no-install-recommends \
    libglu1-mesa \
    openjdk-8-jdk-headless \
    qemu-system-x86 \
    unzip \
    wget >/dev/null \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*
# http://stackoverflow.com/a/37604675/624706

# Download basic Android command line tools
# Get latest version name from https://developer.android.com/studio/index.html#downloads
ARG SDK_ARCHIVE_VERSION
RUN cd /opt \
    && wget --output-document=android-sdk.zip --quiet https://dl.google.com/android/repository/sdk-tools-linux-${SDK_ARCHIVE_VERSION}.zip \
    && unzip -q android-sdk.zip -d android-sdk-linux \
    && rm -f android-sdk.zip

# Add enviroment variables 
# https://developer.android.com/studio/command-line/variables#envar
ENV ANDROID_HOME /opt/android-sdk-linux
ENV ANDROID_SDK_ROOT /opt/android-sdk-linux
# /tools/bin - sdkmanager, avdmanager
# /platform-tools - adb
# /emulator - emulator, emulator-check 
ENV PATH ${ANDROID_SDK_ROOT}/emulator:${ANDROID_SDK_ROOT}/tools/bin:${ANDROID_SDK_ROOT}/platform-tools:${PATH}

# Update AndroidSDK
# Get ids from sdkmanager --list
RUN yes 'y' | sdkmanager --licenses >/dev/null \
    && yes 'y' | sdkmanager "emulator" "platform-tools" "tools" >/dev/null

# GO to workspace
WORKDIR /opt/workspace

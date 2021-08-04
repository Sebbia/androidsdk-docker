FROM ubuntu:20.04

RUN dpkg --add-architecture i386 && \
    apt-get update -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y wget unzip curl cmake git libncurses5:i386 libstdc++6:i386 zlib1g:i386 openjdk-8-jdk-headless
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

# https://developer.android.com/studio/index.html
ENV ANDROID_SDK_ZIP commandlinetools-linux-6858069_latest.zip
ENV ANDROID_SDK_URL https://dl.google.com/android/repository/${ANDROID_SDK_ZIP}

ENV ANDROID_HOME /root/Android/sdk
ENV ANDROID_SDK_ROOT ${ANDROID_HOME}

RUN set -xe \
    && mkdir -p ${ANDROID_SDK_ROOT} \
    && cd ${ANDROID_SDK_ROOT} \
    && wget -q ${ANDROID_SDK_URL} --output-document=${ANDROID_SDK_ZIP} \
    && unzip -qq ${ANDROID_SDK_ZIP} -d ${ANDROID_SDK_ROOT} \
    && mkdir latest \
    && mv ${ANDROID_SDK_ROOT}/cmdline-tools/* ${ANDROID_SDK_ROOT}/latest \
    && mv ${ANDROID_SDK_ROOT}/latest ${ANDROID_SDK_ROOT}/cmdline-tools/latest/ \
    && rm ${ANDROID_SDK_ZIP}

ENV PATH ${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin:${PATH}

ENV ANDROID_TOOLS build-tools;30.0.3 platforms;android-30

RUN for TOOL in ${ANDROID_TOOLS}; do yes | sdkmanager "$TOOL"; done

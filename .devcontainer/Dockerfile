# https://hub.docker.com/r/cirrusci/android-sdk
# https://github.com/cirruslabs/docker-images-android/blob/master/sdk/30/Dockerfile
ARG android_sdk_ver=30

FROM cirrusci/android-sdk:${android_sdk_ver}

ARG flutter_ver=3.3.8
ARG build_rev=0
ARG ANDROID_STUDIO_VERSION=4.2.2
ARG JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
ARG USER="android"
ARG  FLUTTER_URL="https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_3.3.8-stable.tar.xz"

CMD ["bash"]

RUN apt-get -y update
RUN sudo apt-get install software-properties-common apt-transport-https -y
RUN apt-get -y update

RUN sudo add-apt-repository universe
RUN sudo add-apt-repository multiverse
RUN apt-get -y update
RUN apt-get -y upgrade

# RUN add-apt-repository ppa:git-core/ppa
# RUN add-apt-repository ppa:git-core/candidate
# RUN add-apt-repository ppa:mozillateam/ppa
# RUN  sudo add-apt-repository ppa:maarten-fonville/android-studio -y
# RUN apt-get -y update
# RUN apt-get -y upgrade

# RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EA8CACC073C3DB2A
# RUN apt-get -y update

# Install Flutter
ENV FLUTTER_HOME=/usr/local/flutter \
    FLUTTER_VERSION=${flutter_ver} \
    PATH=$PATH:/usr/local/flutter/bin:/usr/local/flutter/bin/cache/dart-sdk/bin
RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y --no-install-recommends --no-install-suggests \
            ca-certificates \
 && update-ca-certificates \
    \
 # Install dependencies for Linux toolchain
 && apt-get install -y --no-install-recommends --no-install-suggests \
            nano \
            build-essential \
            clang cmake \
            lcov \
            libgtk-3-dev liblzma-dev \
            ninja-build \
            pkg-config \
    \
 # Install Flutter itself
 && curl -fL -o /tmp/flutter.tar.xz \
         https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_${flutter_ver}-stable.tar.xz \
 && tar -xf /tmp/flutter.tar.xz -C /usr/local/ \
 && git config --global --add safe.directory /usr/local/flutter \
 && flutter config --enable-android \
                   --enable-linux-desktop \
                   --enable-web \
                   --no-enable-ios \
 && flutter precache --universal --linux --web --no-ios \
 && (yes | flutter doctor --android-licenses) \
 && flutter --version \
 && rm -rf /var/lib/apt/lists/* \
           /tmp/*


# jnstall gpg-agent 2
#chmod -R ug+rw foldername
RUN ["chmod", "777", "-R", "/etc/apt"]
RUN ["cp","/etc/apt/sources.list","/etc/apt/sources.list.bak"]
RUN ["chmod", "777", "-R", "/etc/apt/sources.list.d"]
RUN ["chmod", "777", "/etc/apt/sources.list"]
# CMD ["sh", "-c", 'echo "deb http://security.ubuntu.com/ubuntu focal-security main" > /etc/apt/sources.list.d/gpg-agent.list']
# CMD ["sh", "-c", 'echo "deb http://security.ubuntu.com/ubuntu focal-security main" | tee -a  /etc/apt/sources.list']
# RUN apt-get -y update
# RUN sudo apt-get install -y gpg-agent
# RUN apt-get -y update


# instal google-chrome
CMD ["sh", "-c", 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list']
CMD ["sh", "-c", 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" | tee -a  /etc/apt/sources.list']
# RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key --keyring /etc/apt/trusted.gpg.d/docker-apt-key.gpg add
# RUN apt-get -y update
# RUN apt-get install -y google-chrome-stable
# RUN apt-get -y update

# install android-studio
# RUN sudo add-apt-repository ppa:maarten-fonville/android-studio -y
# CMD ["cd","/usr/local/"]
# RUN apt-cache policy android-studio
# RUN ln -s /studio-data/profile/AndroidStudio$ANDROID_STUDIO_VERSION .AndroidStudio$ANDROID_STUDIO_VERSION
# RUN ln -s /studio-data/Android Android
# RUN ln -s /studio-data/profile/android .android
# RUN ln -s /studio-data/profile/java .java
# RUN ln -s /studio-data/profile/gradle .gradle


# EXPOSE 3000


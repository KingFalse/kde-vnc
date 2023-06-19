FROM debian:bookworm
LABEL authors="KingFalse <yzsl@live.com>"

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    echo keyboard-configuration keyboard-configuration/layout select 'English (US)' | debconf-set-selections && \
    echo keyboard-configuration keyboard-configuration/layoutcode select 'us' | debconf-set-selections && \
    echo "resolvconf resolvconf/linkify-resolvconf boolean false" | debconf-set-selections && \
    apt update && \
    apt install -y novnc desktop-base plasma-desktop --no-install-recommends qml-module-qt-labs-platform kinfocenter systemsettings kscreen python3-pip kwin-x11 dolphin konsole tigervnc-standalone-server tigervnc-xorg-extension dbus-x11 fonts-noto-cjk fonts-noto-cjk-extra firefox-esr && \
    apt clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    groupadd admin && \
    useradd -G admin,video -ms /bin/bash -c "DEBIAN User" debian && \
    echo 'root: ' | chpasswd && \
    echo 'debian: ' | chpasswd && \
    echo 'debian ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
    apt-get clean && \
    mkdir /run/debian && \
    chown debian:debian /run/debian && \
    chmod 7700 /run/debian

ENV DISPLAY=:0 \
    SCR_WIDTH=1600 \
    SCR_HEIGHT=900 \
    SCR_DEPTH=32 \
    KDE_FULL_SESSION=true \
    SHELL=/bin/bash \
    HOME=/home/debian \
    XDG_RUNTIME_DIR=/run/debian

USER debian

WORKDIR /home/debian

EXPOSE 6080
EXPOSE 5900

CMD Xvnc :0 -geometry "$SCR_WIDTH"x"$SCR_HEIGHT" -depth $SCR_DEPTH -SecurityTypes none -AlwaysShared & /usr/share/novnc/utils/novnc_proxy & startplasma-x11
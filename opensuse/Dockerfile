FROM opensuse/tumbleweed
LABEL authors="KingFalse <yzsl@live.com>"

RUN zypper --non-interactive refresh && \
    zypper --non-interactive install shadow sudo xorg-x11-Xvnc-novnc python3-pip python3-cryptography python3-PyJWT \
    patterns-kde-kde_plasma yast2-packager xdg-utils libyui-qt-pkg plasma5-defaults-openSUSE noto-sans-sc-fonts-full konsole dolphin ark kate MozillaFirefox MozillaFirefox-branding-openSUSE && \
    zypper clean --all && rm -rf /var/cache/zypp/* /var/log/zypper.log && \
    groupadd admin && \
    useradd -G admin,video,audio -ms /bin/bash -c "SUSE User" suse && \
    echo 'root: ' | chpasswd && \
    echo 'suse: ' | chpasswd && \
    echo 'suse ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
    mkdir /run/suse && \
    chown suse:suse /run/suse && \
    chmod 7700 /run/suse

ENV DISPLAY=:0 \
    SCR_WIDTH=1600 \
    SCR_HEIGHT=900 \
    SCR_DEPTH=32 \
    KDE_FULL_SESSION=true \
    SHELL=/bin/bash \
    HOME=/home/suse \
    XDG_RUNTIME_DIR=/run/suse \
    TZ=Asia/Shanghai

USER suse

WORKDIR /home/suse

EXPOSE 6080
EXPOSE 5900

CMD rm -rf /tmp/.X0-lock & Xvnc :0 -ac -geometry "$SCR_WIDTH"x"$SCR_HEIGHT" -depth $SCR_DEPTH -SecurityTypes none -AlwaysShared & novnc_server & dbus-run-session startplasma-x11
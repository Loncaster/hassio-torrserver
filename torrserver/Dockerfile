ARG BUILD_ARCH
FROM ghcr.io/hassio-addons/base/${BUILD_ARCH}:21.0.1

ARG BUILD_ARCH
ARG BUILD_VERSION

LABEL \
  io.hass.version="${BUILD_VERSION}" \
  io.hass.type="app" \
  io.hass.arch="${BUILD_ARCH}"

ENV TS_CONF_PATH="/config" \
    TS_TORR_DIR="/config/torrents"

RUN wget -q -O /usr/bin/torrserver \
      "https://github.com/Loncaster/hassio-torrserver/releases/download/2.0.1-MatriX.143/torrserver-${BUILD_ARCH}" \
  && case "${BUILD_ARCH}" in \
       aarch64) echo "9fbb4ec1f9f3c8cf424fe868d32b1d14d1d1356d81a067bc957b4c80f95108f0  /usr/bin/torrserver" | sha256sum -c - ;; \
       amd64) echo "a7ff353b895b8df52339b02126f2bd5b17c1c3da2245dfe8163208000bb82bed  /usr/bin/torrserver" | sha256sum -c - ;; \
       *) exit 1 ;; \
     esac \
  && chmod a+x /usr/bin/torrserver

COPY .build/rootfs /

RUN chmod a+x /run.sh

CMD [ "/run.sh" ]

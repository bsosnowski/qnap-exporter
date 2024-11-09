ARG TELEGRAF_VERSION
FROM telegraf:$TELEGRAF_VERSION

ARG TELEGRAF_VERSION
ARG TARGETPLATFORM
ARG BUILD_DATE
ARG REVISION
ARG VERSION
ARG REF

ENV TELEGRAF_VERSION=$TELEGRAF_VERSION
ENV TARGETPLATFORM=${TARGETPLATFORM}
ENV BUILD_DATE=${BUILD_DATE}
ENV REVISION=${REVISION}
ENV VERSION=${VERSION}
ENV REF=${REF}

LABEL org.opencontainers.image.version="${VERSION}" \
      org.opencontainers.image.authors="bartosz.sosnowski" \
      org.opencontainers.image.created="${BUILD_DATE}" \
      org.opencontainers.image.url="https://github.com/bsosnowski/qnap-exporter" \
      org.opencontainers.image.documentation="https://github.com/bsosnowski/qnap-exporter/blob/main/README.md" \
      org.opencontainers.image.source="https://raw.githubusercontent.com/bsosnowski/qnap-exporter/refs/heads/main/docker/Dockerfile" \
      org.opencontainers.image.revision="${REVISION}" \
      org.opencontainers.image.ref.name="${REF}" \
      org.opencontainers.image.title="Qnap Exporter" \
      org.opencontainers.image.description="SNMP Qnap Exporter" \
      arch="${TARGETPLATFORM}" \
      telegraf.version="${TELEGRAF_VERSION}"

RUN echo "deb http://deb.debian.org/debian bookworm main contrib non-free" >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get install --yes --no-install-recommends snmp-mibs-downloader && \
    rm -rf /var/lib/apt/lists/*

COPY NAS.mib QTS.mib /usr/share/snmp/mibs/

COPY --chmod=755 entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

RUN download-mibs && sed -i "s/^\(mibs *:\).*/#\1/" /etc/snmp/snmp.conf

ENTRYPOINT ["/entrypoint.sh"]
CMD ["telegraf"]

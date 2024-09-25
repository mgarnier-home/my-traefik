FROM alpine:3.17
RUN apk --no-cache add ca-certificates tzdata

COPY dist /binaries

RUN set -ex; \
  apkArch="$(apk --print-arch)"; \
  echo "Test : $apkArch"; \
  case "$apkArch" in \
    armv7) arch='arm' ;; \
    aarch64) arch='arm64' ;; \
    x86_64) arch='amd64' ;; \
    *) echo >&2 "error: unsupported architecture: $apkArch"; exit 1 ;; \
  esac; \
  cp "/binaries/traefik_linux-$arch" /usr/local/bin/traefik; \
	rm -rf /binaries; \
  chmod +x /usr/local/bin/traefik;
COPY my-traefik/entrypoint.sh /
RUN chmod +x /entrypoint.sh
EXPOSE 80
ENTRYPOINT ["/entrypoint.sh"]
CMD ["traefik"]

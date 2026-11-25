# Bodleian Secure Reading Room
#
# A self-hosted Mirador IIIF viewer for reading digitised books in the browser.
# Mirador is pulled from npm as a single, self-contained UMD bundle and served
# as static files by nginx, so the image needs no build toolchain at runtime.
#
# Usage:
#   docker run --rm -p 8080:80 bodleian-secure-reading-room
#   open http://localhost:8080/?manifest=<iiif-manifest-url>

ARG MIRADOR_VERSION=4.3.0

FROM alpine:3.23.3 AS mirador
ARG MIRADOR_VERSION
RUN apk add --no-cache curl \
 && curl -fsSL "https://registry.npmjs.org/mirador/-/mirador-${MIRADOR_VERSION}.tgz" -o /tmp/mirador.tgz \
 && tar -xzf /tmp/mirador.tgz -C /tmp \
 && mkdir -p /out \
 && cp /tmp/package/dist/mirador.min.js /out/mirador.min.js

FROM nginx:1.27-alpine
COPY --from=mirador /out/mirador.min.js /usr/share/nginx/html/mirador.min.js
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80

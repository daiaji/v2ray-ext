FROM alpine AS builder

RUN apk update \
    && apk add --no-cache bash ca-certificates curl unzip \
    && curl $CURLPROXY -fsSL https://install.direct/go.sh | bash -s -- $V2RAYPROXY \
    && curl $CURLPROXY -fsSLo /usr/bin/v2ray/h2y.dat https://raw.githubusercontent.com/ToutyRater/V2Ray-SiteDAT/master/geofiles/h2y.dat

FROM scratch

LABEL maintainer "Darian Raymond <admin@v2ray.com>"

COPY --from=builder /usr/bin/v2ray/ /usr/bin/v2ray/
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=builder /etc/v2ray/config.json /etc/v2ray/config.json

ENV PATH /usr/bin/v2ray:$PATH

ENTRYPOINT [ "v2ray" ]
CMD ["-config=/etc/v2ray/config.json"]

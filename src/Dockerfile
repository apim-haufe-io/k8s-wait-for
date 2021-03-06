FROM alpine:3.7

LABEL maintainer="Michal Orzechowski <orzechowski.michal@gmail.com>, Martin Danielsson <martin.danielsson@haufe-lexware.com>"

ENV KUBE_LATEST_VERSION="v1.10.1"

RUN apk add --update ca-certificates \
 && apk add --update -t deps curl\
 && curl -L https://storage.googleapis.com/kubernetes-release/release/${KUBE_LATEST_VERSION}/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
 && chmod +x /usr/local/bin/kubectl \
 && apk del --purge deps \
 && apk add --update jq \
 && rm /var/cache/apk/* \
 && mkdir -p /usr/src/app

ADD k8s-tool.sh /usr/local/bin/k8s-tool.sh
ADD git_branch /usr/src/app/git_branch
ADD git_last_commit /usr/src/app/git_last_commit

ARG VCS_REF
ARG BUILD_DATE

# Metadata
LABEL org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/apim-haufe-io/wicked.k8s-tool" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.docker.dockerfile="/src/Dockerfile"

ENTRYPOINT ["k8s-tool.sh"]

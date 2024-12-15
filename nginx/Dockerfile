FROM ubuntu:24.04

RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y \
        ca-certificates \
        curl \
        gnupg2 \
        lsb-release \
        ubuntu-keyring

RUN curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor \
        | tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null \
    && echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
            http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" \
            | tee /etc/apt/sources.list.d/nginx.list

RUN apt-get update \
	&& apt-get install --no-install-recommends --no-install-suggests -y \
        nginx \
	    nginx-module-otel \
	&& apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log

CMD ["nginx", "-g", "daemon off;"]

FROM alpine:3.17

RUN set -xe; \
  # install dependencies
  # bash busybox-initscripts busybox-suid py3-pip; \
  apk add --no-cache \
  bash busybox-openrc busybox-suid py3-pip; \
  # install build dependencies
  apk add --no-cache --virtual .build-deps \
  gcc linux-headers libffi-dev musl-dev rust cargo openssl-dev python3-dev; \
  # update pip, acme, certbot/cloudflare 
  pip install --upgrade --no-cache-dir pip acme certbot-dns-cloudflare; \
  # remove build dependencies
  apk del .build-deps; rm -rf /root/.cargo /root/.cache/pip; \
  # turn on cron service
  rc-update add crond;

COPY rootfs/usr/local/bin/* /usr/local/bin/
COPY rootfs/initjobs.d/jobs.txt /initjobs.d/jobs.txt

# Configure the cloudflare secrets
ENTRYPOINT [ "entrypoint.sh" ]

# Run the command on container startup
CMD ["cron.sh"]

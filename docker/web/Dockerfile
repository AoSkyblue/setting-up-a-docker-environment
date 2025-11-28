FROM nginx:1.28-alpine

ENV TZ Asia/Tokyo

COPY ./docker/web/default.conf /etc/nginx/conf.d/default.conf

# Install openssl for dummy cert generation
RUN apk add --no-cache openssl

COPY ./docker/web/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
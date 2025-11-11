FROM  nginx:1.28.0-alpine

COPY docker/images/editor-ui/nginx.conf /etc/nginx/conf.d/default.conf

COPY packages/frontend/editor-ui/dist /usr/share/nginx/html

RUN chown -R nginx:nginx /usr/share/nginx/html

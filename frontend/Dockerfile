# Stage: runtime - serve static build with Nginx
FROM nginx:alpine

# Install envsubst for runtime templating
RUN apk add --no-cache gettext

# Copy template config and entrypoint
COPY nginx.conf.template /etc/nginx/conf.d/default.conf.template
COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh

# Copy pre-built frontend assets
COPY build /usr/share/nginx/html

# Default environment values (can be overridden at runtime)
ENV BACKEND_URL=http://backend:8080 \
    BRAND_NAME=Whaticket \
    BRAND_SHORT_NAME=Whaticket \
    BRAND_THEME_COLOR=#000000 \
    BRAND_BACKGROUND_COLOR=#ffffff

# Nginx listens on 80 by default
EXPOSE 80

# Start via entrypoint to render config and apply branding
CMD ["/docker-entrypoint.sh"]

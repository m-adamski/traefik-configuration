# Traefik Docker configuration

Traefik documentation page: https://doc.traefik.io/traefik/

## Containers configuration
Sample configuration of all containers to be handled by traefik.

```yaml
version: "3.9"

services:
  example:
    image: example/example:latest
    container_name: example-container
    labels:
      - traefik.enable=true
      - traefik.port=8080 # Container port for proxy
      - traefik.http.routers.zabbix.rule=Host(`example.com`)
      - traefik.http.routers.zabbix.tls=true
    networks:
      - default
      - reverse-proxy-network
    restart: always
    depends_on:
      - database

networks:
  reverse-proxy-network:
    external: true
  default:
    driver: bridge
    external: false
````

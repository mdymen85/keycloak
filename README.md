# keycloak
Tests with Keycloak information

```
version: '3'

services:
  mysql:
    container_name: mysql
    image: mysql:latest
    environment:
      - MYSQL_ROOT_PASSWORD=mdymen_pass
      - MYSQL_DATABASE=keycloak
    ports:
      - "3306:3306"
    command: --init-file /data/application/init.sql
    volumes:
      - .docker/db/mysql:/var/lib/mysql
      - ./init.sql:/data/application/init.sql
  keycloak:
    container_name: keycloak
    image: quay.io/keycloak/keycloak:21.1.0
    environment:
      - KEYCLOAK_ADMIN=admin
      - KEYCLOAK_ADMIN_PASSWORD=admin
      - KC_DB=mysql
      - KC_DB_USERNAME=root
      - KC_DB_PASSWORD=mdymen_pass
      - KC_DB_URL_HOST=mysql
      - KC_DB_URL_PORT=3306
      - KC_DB_SCHEMA=keycloak
    ports:
      - 8080:8080
    command: start-dev
    depends_on:
      - mysql
```


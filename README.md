## **PhpMyAdmin**

Dockerized PHPMYADMIN

## Usage with docker-compose behind proxy

```shell
version: '2.4'

networks:
  default:
    external:
      name: proxy-tier 
  db-net:
    external:
      name: backend-tier

services:

  phpmyadmin:
    image: pam79/pma
    container_name: phpmyadmin
    volumes:
      - /sessions
      - ./config.user.inc.php:/etc/phpmyadmin/config.user.inc.php
    environment:
      - "PMA_ABSOLUTE_URI=https://pma.example.com/"
      - "VIRTUAL_HOST=pma.example.com"
      - "VIRTUAL_PORT=9000"
    ports:
        - 80:80
    networks: 
      - default
      - db-net
    restart: always
```

## Usage behind reverse proxys

Set the variable **`PMA_ABSOLUTE_URI`** to the fully-qualified path **`https://pma.example.net/`** where the reverse proxy makes phpMyAdmin available.

## Environment variables summary

* `PMA_ARBITRARY` - when set to 1 connection to the arbitrary server will be allowed
* `PMA_HOST` - define address/host name of the MySQL server
* `PMA_VERBOSE` - define verbose name of the MySQL server
* `PMA_PORT` - define port of the MySQL server
* `PMA_HOSTS` - define comma separated list of address/host names of the MySQL servers
* `PMA_VERBOSES` - define comma separated list of verbose names of the MySQL servers
* `PMA_PORTS` - define comma separated list of ports of the MySQL servers
* `PMA_USER` and `PMA_PASSWORD` - define username to use for config authentication method
* `PMA_ABSOLUTE_URI` - define user-facing URI

For more detailed documentation see https://docs.phpmyadmin.net/en/latest/setup.html#installing-using-docker

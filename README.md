# Local proxy

Proxy service to handle multi app development.

Proxy to container with name equals to host without `.loc`:

    pet.loc => pet
    my-site.loc => my-site

Target container should be connected to `proxy` network and had appropriate alias.

## Usage sample

/etc/hosts
    127.0.0.1 pet.loc

docker-compose:
    
    services:
      server:
        build: ./docker/nginx
        image: mage-server
        container_name: mage-server
        volumes:
          - ./src:/var/www/app
        ports:
          - 80
          - 443
        networks:
          default:
          proxy:
            aliases:
              - pet
        depends_on:
          - app
    
    networks:
      default:
      proxy:
        external:
          name: proxy
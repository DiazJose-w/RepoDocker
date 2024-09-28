# RepoDocker
Creamos archivo compose.yml

            version: '3.1'
            services:
              web:
                image: odoo:17.0
                depends_on:
                  - db
                ports:
                  - "8069:8069"
                volumes:
                  - odoo-web-data:/var/lib/odoo
                  - ./config_odoo:/etc/odoo
                  - ./dev_addons:/mnt/extra-addons
                  - ./log:/var/log/odoo
                environment:
                  - HOST=db
                  - USER=odoo
                  - PASSWORD=odoo
              db:
                image: postgres:latest
                environment:
                  - POSTGRES_DB=postgres
                  - POSTGRES_PASSWORD=odoo
                  - POSTGRES_USER=odoo
                  - PGDATA=/var/lib/postgresql/data/pgdata
                volumes:
                  - odoo-db-data:/var/lib/postgresql/data/pgdata
            volumes:
              odoo-web-data:
              odoo-db-data:

  Creamos módulo con
    -odoo scaffold "nombre_del_modulo"

  Vamos al directorio donde está el archivo que acabamos de crear y ejecutamos:
    - docker-compose up -d

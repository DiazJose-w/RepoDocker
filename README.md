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

  Crear módulo en el directorio dev-addons
-             odoo scaffold "nombre_del_modulo"

  Ejecutar el archivo compose.yml:
-             docker-compose up -d

  Archivos de configuracion en el directorio config_odoo
-             [options]
            addons_path = /mnt/extra-addons
            data_dir = /var/lib/odoo
            admin_passwd = passwd
            logfile = /var/log/odoo/odoo-server.log

  Archivo models.py
-             from odoo import models, fields, api
  
            class modulo_jose(models.Model):
                 _name = 'modulo_jose.modulo_jose'
                 _description = 'modulo_jose.modulo_jose'
            
                 name = fields.Char()
                 value = fields.Integer()
            #     value2 = fields.Float(compute="_value_pc", store=True)
            #     description = fields.Text()
            #
            #     @api.depends('value')
            #     def _value_pc(self):
            #         for record in self:
            #             record.value2 = float(record.value) / 100

  Archivo _manifest_.py
-         # -*- coding: utf-8 -*-
              {
                'name': "moduloJose",
            
                'summary': "Short (1 phrase/line) summary of the module's purpose",
            
                'description': """
                        Long description of module's purpose
                """,
            
                'author': "My Company",
                'website': "https://www.yourcompany.com",
            
                # Categories can be used to filter modules in modules listing
                # Check https://github.com/odoo/odoo/blob/15.0/odoo/addons/base/data/ir_module_category_data.xml
                # for the full list
                'category': 'Uncategorized',
                'version': '0.1',
            
                # any module necessary for this one to work correctly
                'depends': ['base'],
            
                # always loaded
                'data': [
                    'security/ir.model.access.csv',
                    'views/views.xml',
                    'views/templates.xml',
                ],
                # only loaded in demonstration mode
                'demo': [
                    'demo/demo.xml',
                ],
            }    

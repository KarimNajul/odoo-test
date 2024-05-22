# Como instalar odoo


## Instalar odoo en docker compose

### Comandos y archivos a crear:
> Esto no te muestra como instalar docker solo a hacer la instancia de odoo dentro de docker compose

#### Crear odoo_conf:

Como primer paso tenemos que crear un archivo odoo.conf el cual contiene la configuracion de odoo

```
[options]
addons_path = /mnt/extra-addons
data_dir = /var/lib/odoo
; admin_passwd = admin
; csv_internal_sep = ,
; db_maxconn = 64
; db_name = False
; db_template = template1
; dbfilter = .*
; debug_mode = False
; email_from = False
; limit_memory_hard = 2684354560
; limit_memory_soft = 2147483648
; limit_request = 8192
; limit_time_cpu = 60
; limit_time_real = 120
; list_db = True
; log_db = False
; log_handler = [':INFO']
; log_level = info
; logfile = None
; longpolling_port = 8072
; max_cron_threads = 2
; osv_memory_age_limit = 1.0
; osv_memory_count_limit = False
; smtp_password = False
; smtp_port = 25
; smtp_server = localhost
; smtp_ssl = False
; smtp_user = False
; workers = 0
; xmlrpc = True
; xmlrpc_interface = 
; xmlrpc_port = 8070
; xmlrpcs = True
; xmlrpcs_interface = 
; xmlrpcs_port = 8071
```

#### Luego creamos las carpetas dev_addons y log
#### Por ultimo creamos un archivo docker-compose.yaml:

Este contendra toda la configuracion para instalar la instancia de odoo en docker
```
[options]
addons_path = /mnt/extra-addons
data_dir = /var/lib/odoo
; admin_passwd = admin
; csv_internal_sep = ,
; db_maxconn = 64
; db_name = False
; db_template = template1
; dbfilter = .*
; debug_mode = False
; email_from = False
; limit_memory_hard = 2684354560
; limit_memory_soft = 2147483648
; limit_request = 8192
; limit_time_cpu = 60
; limit_time_real = 120
; list_db = True
; log_db = False
; log_handler = [':INFO']
; log_level = info
; logfile = None
; longpolling_port = 8072
; max_cron_threads = 2
; osv_memory_age_limit = 1.0
; osv_memory_count_limit = False
; smtp_password = False
; smtp_port = 25
; smtp_server = localhost
; smtp_ssl = False
; smtp_user = False
; workers = 0
; xmlrpc = True
; xmlrpc_interface = 
; xmlrpc_port = 8070
; xmlrpcs = True
; xmlrpcs_interface = 
; xmlrpcs_port = 8071
```

## Creacion de odoo en docker (no docker compose)

### Comandos para la instalacion

```
sudo docker run -d -v odoo-db:/var/lib/postgresql/data -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=postgres --name db postgres


sudo docker run -v odoo-data:/var/lib/odoo -d -p 8069:8069 --name odoo --link db:db -t odoo
```


## Comando utiles cuando estas haciendo la instalacion

#### Comandos para iniciar y parar el contenedor en docker (sin compose)

```
sudo docker stop odoo
docker start -a odoo
```

#### Si no podes cambiar el puerto local al cual apunta tu contenedor
```
sudo docker exec -u root -it c343c72c8f5e /bin/bash

sed -i 's/xmlrpc_port = 8069/xmlrpc_port = 8070/' /etc/odoo/odoo.conf

exit

sudo docker restart c343c72c8f5e
```

#### Con este comando podes ver el contenido de un archivo desde la consola
```
cat /etc/odoo/odoo.conf
```

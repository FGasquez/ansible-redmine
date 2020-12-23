# Ansible Playbook redmine
Playbook que instala redmine y sus dependencias en ubuntu


# Dependencias
Ansible 2.10.4


# Configuración
En la carpeta `group_vars` están los archivos de configuraciones:
 - common.yml
    - project_dir: el directorio donde se instalara redmine (`{project_dir}/redmine`)
    - url: valor que se pondrá en el `server_name`, por defecto es `localhost`

- guest.yml
    - user: Usuario con el que se utilizará para instalar redmine.

- mysql.yml
    - root_password: la contraseña de root, si no está configurada, se intentará cambiar po esta
    - user: el usuario que utilizará redmine para comunicarse con la base de datos, si no existe, será creado
    - password: la contraseña del usuario
    - dbname: el nombre de la base de datos que utilizará redmine, de no existir, será creada

- redmine.yml
    - url: la url de donde se descargará el zip con la release de redmine
    - version: la versión de redmine que se instalará
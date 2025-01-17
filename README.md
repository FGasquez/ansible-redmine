# Ansible Playbook redmine
Playbook que instala redmine y sus dependencias en ubuntu 18.04


# Dependencias
Las versiones utilizadas en el desarrollo fueron:

- Ansible `2.10.4`
- Vagrant `2.2.14`

# Ejecución

Primero configurar el host en redmine.yml, dejandolo acorde a su archivo hosts, por ejemplo:
```yml
# redmine.yml
- name: install redmine
  hosts: ubuntu
```

```
# hosts
[ubuntu]
localhost:2222 ansible_ssh_user=vagrant
```

## Correr ansible-playbook

```bash
    $ ansible-playbook -i hosts redmine.yml
```

# Roles:

- system: instala las dependecias
- rbenv: instala y configura rbenv
- mysql: instala y configura la base de datos
- redmine: descarga redmine, instala las dependencias y corre las migraciones
- nginx: confiugra el servicio.
- firewall: cierra los puertos.


# Configuración

En la carpeta `vars` están los archivos de configuraciones:
 - common.yml
    - project_dir: el directorio donde se instalara redmine (`{{    project_dir }}/redmine`)
    - url: valor que se pondrá en el `server_name`, por defecto es `localhost`
    - dir_owner: el usuario propietario del directorio de redmine
    - dir_group: El grupo propietario del directorio de redmine
    - ruby_version: la versión de ruby que se utilizará

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

- rbenv.yml
    - repo: la url al repositorio de rbenv
    - root: el path donde se clonará rbenv
    - version: la versión de rbenv que se instalará
    - executable_path: el path donde están los ejecutables de rbenv

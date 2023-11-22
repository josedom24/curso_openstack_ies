# Configuración de instancias con cloud-init

## Configuración de una instancia

La creación de un servidor en IaaS (instancia) es un proceso peculiar, que requiere un tratamiento específico. Se parte de una imagen mínima, sin contraseña establecida y con una configuración totalmente genérica. Y es necesario realizar una configuración de la máquina:
* Imprescindible la configuración inicial:
	* Generación de la clave ssh de la instancia
	* Parámetros de red, hostname, etc.
	* Autenticación del usuario (clave ssh)
* Configuración no esencial:
	* Actualización de los paquetes instalados, instalación de algún paquete,...
	* Creación de algún usuario
	* ...

## cloud-init

**cloud-init: cloud instance initialization**, es un programa que permite realizar la configuración de la instancia al crearse a partir de una imagen. Es el estándar de facto en nube pública o privada, está desarrollado en python y es un proyecto liderado por Canonical.

El paquete `cloud-init` está instalado habitualmente en las imágenes para IaaS. [Documentación cloud-init](https://cloudinit.readthedocs.io).

Una instancia que se inicia o reinicia, puede obtener diferentes tipos de datos, en función del origen de estos:
* **Metadatos**: Obtenidos del **servidor de metadatos** del proveedor de nube (típicamente a través de dirección de enlace local http://169.254.169.254). Incluye las características propias de la instancia: nombre, configuración de red, tamaño de los discos, etc.
* **Datos de usuario (opcional)**: Datos adicionales de configuración que proporciona el usuario de la instancia (**user-data**).
* **Datos del proveedor (opcional)**: Datos adicionales de configuración proporcionados por el proveedor (**vendor-data**).

Cuando se configura una instancia con cloud-init, se siguen los siguientes pasos:

* Se obtiene la información de la configuración de red. Si no existe, se hace una petición DHCP.
* Se redimensiona la partición raíz.
* Se montan las particiones.
* Se generan los números aleatorios.
* Se establece el hostname.
* Se generan las claves ssh del servidor.
* Otras tareas indicadas por medio del **user-data**.

## user-data: cloud-config

Hay varios formatos aceptados para introducir **user-data**, el más habitual es mediante el formato YAML conocido como cloud-config.

Veamos un ejemplo de un script cloud-config:

```yaml
#cloud-config
# Actualiza los paquetes
package_update: true
package_upgrade: true
# Configura el hostname y el fqdn
fqdn: maquina.example.org
hostname: maquina
manage_etc_hosts: true
# Crear dos usuarios, configura el acceso por sudo y añade clave pública ssh
users:
  - name: usuario1
    sudo: ALL=(ALL) NOPASSWD:ALL
    shell: /bin/bash
    ssh_authorized_keys: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQ...
  - name: usuario2
    sudo: ALL=(ALL) NOPASSWD:ALL
    shell: /bin/bash
    ssh_authorized_keys: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQ...
# Cambia las contraseña a los usuarios creados
chpasswd:
  list: |
    root:password
    usuario1:password1
    usuario1:password2
expire: False
```

Este script hace las siguientes configuraciones:

* Actualiza los paquetes.
* Configura el hostname y el fqdn.
* Crear dos usuarios, configura el acceso por sudo y añade clave pública ssh.
* Cambia las contraseña a los usuarios creados.


Puedes acceder a la lista de módulos que puedes usar en cloud-config en la [documentación oficial](https://cloudinit.readthedocs.io/en/latest/topics/modules.html).

## Configuración de cloud-init

En OpenStack Horizon, durante la creación de una instancia podemos indicar el **user-data** en la siguiente pestaña:

![cloud-init](img/cloud-init.png)

Usando la línea de comandos, se indica el fichero de configuración en el parámetro `--user-data`:

	openstack server create --flavor m1.mini \
        --image "Debian 11.0 - Bullseye" \
        --security-group default \
        --key-name clave_jdmr \
        --network "red de josedom" \
        --user-data cloud-config.yaml
        instancia_prueba

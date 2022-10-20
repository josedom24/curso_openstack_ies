# Instalación y uso básico de OpenStack client (OSC)

Otra forma de interactuar con OpenStack es usar un cliente de línea de comandos: *Openstack Client (OSC)*.

## Instalación de OpenStack Client

Para instalar el cliente de OpenStack vamos a usar un entorno virtual de python3:

```
$ python3 -m venv os
(os)$ source os/bin/activate
(os)$ pip install python-openstackclient==5.8.0
```

No hemos instalado la última versión, hemos instalado la versión de OSC que corresponde con la versión yoga de OpenStack que estamos utilizando:

```
(os)$ openstack --version
openstack 5.8.0
```

Ahora necesitamos el fichero de credenciales, para que nos podamos autentificar a nuestro proyecto de OpenStack, para descargar el fichero desde horizon escogemos la siguiente opción:

Imagen

Para cargar las variables de entorno que se definen en ese fichero podemos ejecutar:

```
(os)$ source Proyecto\ de\ josedom-openrc.sh
Please enter your OpenStack Password for project Proyecto de josedom as user josedom: 
```

Y nos pide la contraseña de nuestro usuario que se guardará en otra variable de entorno. Una vez introducida la contraseña podremos usar el comando `openstack` para gestionar los recursos de nuestro proyecto. Por ejemplo para ver las máquinas que tenemos creadas ejecutamos:

```
(os)$ openstack server list
```

## Configuración de las claves ssh con OSC

Para crear una clave ssh con el cliente de Openstack, podemos ejecutar:

```
(os)$ openstack keypair create --public-key ~/.ssh/id_rsa.pub miclave
```

Puedo ver las claves que tengo creadas en mi proyecto, ejecutando:

```
(os)$ openstack keypair list
```

Para aprender más operaciones que podemos realizar con las claves con OSC: [OpenStackClient keypair](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/keypair.html).

## Configuración de los Grupos de seguridad con OSC


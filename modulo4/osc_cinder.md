# Gestión de volúmenes con OpenStack client (OSC)

## Asociación de un volumen a una instancia

1. Vamos a crear un volumen de 1 GiB:

        openstack volume create --size 1 mi_disco1

    Podemos ver los volúmenes con:

        openstack volume list

    Para ver todas las operaciones que podemos hacer sobre los volúmenes: [OpenStackClient volume](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/volume.html).

2. A continuación vamos a asociarlo a nuestra instancia:

        openstack server add volume --device /dev/sdb instancia_prueba mi_disco1

3. Para desasociar el volumen de la instancia:

        openstack server remove volume instancia_prueba mi_disco1

## Creación de una instancia con el disco raíz sobre un volumen

1. Visualizamos la lista de imágenes y de sabores que tenemos en 
nuestro sistema: 

    	openstack image list
    	openstack flavor list

2. Creamos un volumen *arrancable* de 8 GiB que contenga la imagen:

        openstack volume create --bootable --size 8 --image "Debian 11.0 - Bullseye" disco_debian

3. Creamos una nueva instancia con este volumen:

        openstack server create --flavor vol.mini \
        --volume disco_debian \
        --security-group default \
        --key-name clave_jdmr \
        --network "red de josedom" \
        instancia_prueba2

    Nota: He escogido el sabor `vol.mini` que tiene 0 de disco duro, porque estoy usando un volumen.

## Creación de una instantánea de un volumen

1. Creamos una instantánea de volumen

		openstack volume snapshot create --volume mi_disco1 copia_mi_disco1
		
2. Listamos las instantáneas

		openstack volume snapshot list
		
3. Creamos un nuevo volumen a partir de la instantánea

		openstack volume create --snapshot copia_mi_disco1 disco2
		
4. Borramos el snapshot y el volumen creado

	Si intentamos borrar el volumen desde el que hemos creado la instantánea:

		openstack volume delete mi_disco1
		Invalid volume: Volume still has 1 dependent snapshots. (HTTP 400) (Request-ID: req-917a4f06-8874-4e59-a693-122006454d90)

	Debemos borrar primero el snapshot y posteriormente el volumen:

		openstack volume snapshot delete copia_mi_disco1
		openstack volume delete mi_disco1

    Puedes ver las operaciones que podemos hacer con los snapshots en [OpenStackClient volume snapshot](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/volume-snapshot.html).
    
## Extender el tamaño de un volumen

Vamos a redimensionar el tamaño de un volumen:

		openstack volume set --size 2 disco2

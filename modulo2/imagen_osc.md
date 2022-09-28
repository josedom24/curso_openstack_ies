# Gestión de imágenes con OpenStack client (OSC)

## Crear una nueva imagen

Para subir la imagen:

	openstack image create --container-format=bare --disk-format=qcow2 \
	 --file cirros-0.5.1-x86_64-disk.img "Cirros 0.5.1"

Para que sea visible por todos:

    openstack image set --community "Cirros 0.5.1"

## Listar las imágenes disponibles

	openstack image list

## Ver detalles de la imagen

	openstack image show "Cirros 0.5.1"

## Borrar la imagen

	openstack image delete "Cirros 0.5.1"

## Documentación

* [OpenStackClient image](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/image-v2.html)

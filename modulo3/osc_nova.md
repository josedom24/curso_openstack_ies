# Gestión de instancia con OpenStack client (OSC)

## Gestión de instancias con OpenStack client (OVS)

Vamos a ver todos los pasos que necesitamos para crear una instancia: 

1. Suponemos que ya tenemos un par de claves subida a nuestro proyecto, la podemos ver:

        openstack keypair list
    
    Podemos hacer más operaciones sobre las claves almacenadas en nuestro proyecto: [OpenStackClient keypair](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/keypair.html).

2. Necesitamos saber que grupo de seguridad vamos a configurar la instancia:

        openstack security group list
    
    Podemos ver las reglas definida en el grupo de seguridad `default`:

        openstack security group rule list default
    
    Incluso podemos añadir una nueva regla en el grupo de seguridad `default`:

        openstack security group rule create --protocol tcp --remote-ip 0.0.0.0/0 --dst-port 80 default
    
    Podemos ver las operaciones sobre los grupos de seguridad: [OpenStackClient security group](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/security-group.html) y [OpenStackClient security group rule](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/security-group-rule.html).

3. Obtenemos la información de las imágenes, sabores (tipos de
servidores) y redes que tenemos disponibles.

        openstack image list
        openstack flavor list
        openstack network list

    La gestión de las imágenes ya la hemos estudiado, la gestión de redes la veremos en el próximo apartado, para la gestión de los sabores puedes acceder a [OpenStackClient flavor](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/flavor.html).

4. Ya podemos crear nuestra instancia:

        openstack server create --flavor m1.mini \
        --image "Debian 11.0 - Bullseye" \
        --security-group default \
        --key-name clave_jdmr \
        --network "red de josedom" \
        instancia_prueba

5. Por último reservamos una nueva ip flotante del pool "ext-net" y la
asignamos a la instancia para poder acceder a ella desde el exterior:

    Podemos ver las ip flotantes que tenemos reservadas:

        openstack floating ip list

    Podemos solicitar otra ip flotante:

        openstack floating ip create ext-net

    Podemos ver todas las operaciones que podemos hacer con la ip flotantes en [OpenStackClient floating ip](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/floating-ip.html).

    Y ahora asignamos una ip flotante a nuestra instancia:

        openstack server add floating ip instancia_prueba 172.22.201.111
    
    Puedes ver todas las operaciones que podemos hacer sobre las instancias en [OpenStackClient server](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/server.html).



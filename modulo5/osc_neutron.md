# Gestión de redes con OpenStack client (OSC)

## Crear redes, subredes y router

1. Vemos las redes, subredes y routers que tenemos en nuestro
proyecto:

        openstack network list
        openstack subnet list
        openstack router list

2. Creamos una red de nombre *mi_red* con una subred asociada con el direccionamiento 192.168.0.0/24:

        openstack network create mi_red
        openstack subnet create --network mi_red --subnet-range 192.168.0.0/24 --dns-nameserver 172.22.0.1 mi_subred

    Podemos configurar la subred con más detalle (rango DHCP, puerta de enlace,...) para ello:

        openstack subnet create --help

3. Creamos un nuevo router (mi_router), que vamos a conectar con la red externa y con la subred anteriormente creada:

        openstack router create mi_router

    Ahora conectamos el router e la red externa:

        openstack router set mi_router --external-gateway ext-net
    
    Ahora enlazamos con la red creada:

        openstack router add subnet mi_router mi_subred

4. Si queremos conectar una instancia a la red que hemos creado, ejecutaremos:

        openstack server add network nombre_instancia mi_red

5. Podemos crear una nueva instancia conectada a la red que hemos creado:

        openstack server create --flavor m1.mini \
        --image "Debian 11.0 - Bullseye" \
        --security-group default \
        --key-name clave_jdmr \
        --network mi_red \
        instancia_prueba3

Podemos ver todas las acciones que podemos hacer sobre las redes, subredes y router en:

* [OpenStackClient network](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/network.html)
* [OpenStackClient subnet](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/subnet.html)
* [OpenStackClient router](https://docs.openstack.org/python-openstackclient/latest/cli/command-objects/router.html)

## Trabajar con puertos

1. Podemos listar los puertos de una red, o de un router o de una instancia:

        openstack port list --network mi_red
        openstack port list --router mi_router
        openstack port list --server instancia_prueba2

2. Podemos crear un puerto de la siguiente manera:

        openstack port create --network mi_red mi_port

    En este caso como tenemos un DHCP en la subred se le asignara una IP de forma dinámica, si queremos indicar una ip fija:

        openstack port create --network mi_red --fixed-ip ip-address=192.168.0.100 mi_port

3. A partir de un puerto creado, podemos usarlo para crear por ejemplo una instancia que use dicho puerto:

        openstack server create --flavor m1.mini \
        --image "Debian 11.0 - Bullseye" \
        --security-group default \
        --key-name clave_jdmr \
        --port mi_port \
        instancia_prueba4

4. A partir de un puerto creado, podemos añadir una interfaz a un router:

        openstack port create --network mi_red --fixed-ip ip-address=192.168.0.200 mi_port2
        openstack router create mi_router3
        openstack router add port mi_router3 mi_port2

5. De manera similar podemos añadir una nueva interfaz a una instancia correspondiente al puerto que hemos creado:

        openstack port create --network mi_red --fixed-ip ip-address=192.168.0.201 mi_port3
        openstack server add port nombre_instancia mi_port3

## Deshabilitar el grupo de seguridad de una instancia

1. Si queremos quitar el grupo de seguridad a una instancia, para quitar el cortafuego que le hemos asignado:

    Lo primero es quitar el grupo de seguridad a la instancia:

        openstack server remove security group instancia_prueba4 default

    Ahora la instancia tiene todos los puertos cerrado, por lo que a continuación hay que deshabilitar la seguridad del puerto:

        openstack port set --disable-port-security mi_port
    
    Nota: Si el puerto no tiene nombre tenemos que indicar el id del puerto.

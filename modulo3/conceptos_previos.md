# Conceptos previos

## Imagen

Una imagen de máquina virtual, o de forma abreviada una imagen, es un
fichero que contiene un disco virtual con un sistema operativo con la
configuración mínima para poder operar adecuadamente dentro de una
nube de infraestructura.

## Instancia 

Una instancia es un servidor virtual que se ejecuta dentro de la nube
de infraestructura y que se basa en una imagen, de hecho una instancia
es inicialmente un clon de una imagen.

## Tipo de instancia o sabor

Define inicialmente las características de la instancia, como el
número de cores virtuales (vCPU), cantidad de memoria RAM o tamaño del
disco duro del sistema operativo.

Partiendo de una misma imagen se consiguen instancias con diferentes
características al crearlas de diferente tipo.

## IP fija

Dirección IP interna de la instancia y que se define en el momento de
la creación de la instancia. La dirección IP fija se utiliza para la
comunicación interna de la instancia y su valor no varía durante la
vida de la instancia, de ahí que reciba el nombre de IP fija.

## IP flotante 

Dirección IP que se asigna a una instancia después de crearla y que se
utiliza para la comunicación desde el exterior. No todas las
instancias tienen por qué tener una IP flotante.

## Grupo de Seguridad (Cortafuegos)

Conjunto de reglas de iptables que actúan como cortafuegos a nivel de
la instancia.

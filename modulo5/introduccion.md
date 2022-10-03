# Introducción a la virtualización de redes

## Redes virtuales

Normalmente entendemos las redes virtuales, que creamos dentro de un equipo y que nos permite conectar las máquinas virtuales entre sí, aislar máquinas virtuales en redes distintas o para que tengan conexión con el exterior.

Las redes virtuales de este tipo se definen dentro del equipo que actúa como hipervisor y se comunican con el exterior a través de las interfaces de red físicas de este equipo o utilizando bridges virtuales.

## Virtualización de redes, redes definidas por software y virtualización de las funciones de red

El campo de las redes está últimamente revolucionado y se escuchan por todos sitios tres términos o sus equivalentes siglas en inglés:

* **Virtualización de redes** o *network virtualization* (NV)
* **Redes definidas por software** o *software defined networks* (SDN)
* **Virtualización de las funciones de red** o *network function virtualization* (NFV). 

Este conjunto de tecnologías ofrecen diferencias respecto a las redes clásicas o las redes virtuales definidas como
hasta ahora. Algunas de estas diferencias son:

* Todos los elementos de la red pasan a controlarse de forma centralizada.
* Los elementos de la red pueden entenderse unos con otros independientemente del fabricante.
* Se crea una sola red a nivel lógico que se divide en las redes necesarias.
* La misma red virtual puede estar definida en varios hipervisores y controlarse de forma centralizada.
* Las funciones de red como cortafuegos, balanceadores, QoS, etc. se pueden definir por software, ubicar en cualquier punto de la red y controlar de forma centralizada.

OpenStack ya posee muchas de estas características en su gestión de las redes. OpenStack neutron proporciona estas características: creación de redes privadas en cada uno de los proyectos, gestión de routers, comunicación de las instancias aunque se estén ejecutando en nodos de computación diferentes, configuración de cortafuegos, ...

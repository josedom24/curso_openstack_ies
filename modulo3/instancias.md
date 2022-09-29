# Creación de instancias a partir de una imagen

El objetivo de esta sección es mostrar es la creación de una instancia GNU/Linux
a partir de una de las imágenes disponibles. Para ello accedemos al apartado
**Instancias** > **Lanzar instancia** y a continuación tenemos
que indicar los siguientes datos:

### Detalles 

![instancias](img/instancias1.png)

Indicamos el **nombre de la instancia**, la **descripción**, la zona de disponibilidad (en nuestro caso *nova*) y el número de instancias que se van a crear.

### Origen

![instancias](img/instancias2.png)

Seleccionamos el origen que vamos a usar para crear la instancia. Tenemos cuatro posibilidades:

* **Imagen**: Es la que vamos a escoger en este apartado. Elegimos de la lista la imagen que vamos a usar.
* **Instantánea de instancia.**
* **Instantánea de volumen.**
* **Volumen**

En las dos primeras opciones no da la posibilidad de **crear un nuevo volumen** (lo estudiaremos en el módulo de almacenamiento). En las dos últimas posibilidades nos da la opción de **eliminar el volumen** al eliminar la instancia.

## Sabor

![instancias](img/instancias3.png)

Se escoge el sabor de la instancia que vamos a crear. El sabor determina las características de VCPUS, memoria RAM y tamaño de disco que tendrá la instancia. Cada instancia nos determina 4 valores:

* Número de **VCPUS**.
* Tamaño de la memoria **RAM**.
* Tamaño del **disco raíz** principal.
* Tamaño de un segundo disco que llama **disco efímero**.

En el instituto tenemos tres tipos de sabores:

* **m1**: Son sabores pensadas para las máquinas Linux sin entorno gráfico.
* **vol**: Son sabores que se deben usar al crear instancias sobre volúmenes, en este caso los tamaños de discos están a 0, porque serán del tamaño que creemos el volumen.
* **win**: Son sabores pensadas para las máquinas Windows.

### Redes

![instancias](img/instancias4.png) 

En este apartado escogemos las redes definidas en el proyecto donde estará conectada la instancia. Si sólo tenemos una se escoge por defecto.

### Puertos de red

![instancias](img/instancias5.png) 

Si hemos creado algún puerto (lo estudiaremos en el módulo de redes) podrémos escogerlos para especificar la configuración de red de la instancia.

### Grupos de Seguridad

![instancias](img/instancias6.png) 

Se escoge los grupos de seguridad que van a configurar el cortafuego de la instancia. Si sólo tenemos uno definido, se escogerá por defecto.

### Par de claves

![instancias](img/instancias7.png) 

Seleccionamos la clave pública que hemos subido a OpenStack para que se inyecte a la instancia y nos permita el acceso. Si sólo tenemos definida una clave, se escogerá por defecto.

### Configuración

![instancias](img/instancias8.png) 

En este apartado podemos introducir un script para configurar de forma automática la instancia por medio de **cloud-init**. Lo estudiaremos en un apartado posterior.

### Opciones restantes

Las opciones restante nos la vamos a estudiar en este curso.

## Asignación de IP flotante

Una vez que hemos creado la instancia:

![instancias](img/instancias9.png) 

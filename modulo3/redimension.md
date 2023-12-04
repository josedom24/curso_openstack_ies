# Redimensión y reconstrucción de instancias

## # Redimensión de instancias

Esta acción sirve para cambiar las características hardware del servidor, modificando el tipo de instancia (sabor) asociado al mismo. Este proceso también se conoce como escalado vertical o *scale up*.

Para Realizar estas operaciones el usuario deberá seleccionar la instancia y elegir la opción de **Redimensionar instancia**.

Este proceso se realiza en dos pasos, ya que en un primer paso se verifica que es posible realizarlo y si se concluye satisfactoriamente el servidor pasa al estado VERIFY_RESIZE tras el que se le ofrecen al usuario dos opciones: **Confirmar la redimensión** o **Revertir la redimensión**.

![redimensión](img/redimension.png)

## Reconstrucción de instancia

La reconstrucción de una instancia es un mecanismo que nos permite rehacer una instancia con otra imagen sin perder la ip fija y otros metadatos.

![reconstruccion](img/reconstruccion.png)

Se crea otra instancia con la misma IP flotante que la primera, a partir de la imagen que se ha indicado, el disco raíz de la primera instancia se conectará como disco secundario a esta nueva instancia, con lo que podremos acceder al disco e intentar recuperar el error que tengamos.

# Gestión imágenes con Horizon

Una imagen de máquina virtual, o de forma abreviada una imagen, es un fichero que contiene un disco virtual con un sistema operativo con la configuración conocidos los relacionados con los hipervisores más conocidos: VMDK para VMware, qcow2 para QEMU/KVM, etc. o el formato (ami-ari-aki propio de Xen y muy habitual en IaaS por ser el que utiliza Amazon EC2).

Teniendo en cuenta el enfoque de recursos compartidos que se utiliza en IaaS, es muy frecuente que se compartan entre todos los usuarios un conjunto de imágenes genéricas con los sistemas operativos más habituales, es lo que se conoce como **imágenes públicas**. También es posible que el usuario suba o gestione sus propias imágenes, con el grado de configuración que desee.

Las imágenes se utilizan para instanciar las máquinas virtuales que realmente utiliza el usuario.

## Catálogo de imágenes

Para ver las imágenes que inicialmente podemos utilizar abrimos la opción de **Imágenes**:

![Imágenes](img/01.png)

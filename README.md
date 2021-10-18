# Intranet
**Proyecto II** 

###### Mario Field     7690 17 20612
###### Daniel Paniagua 7690 17 6640



## Openvpn

OpenVPN es un cliente/servidor VPN (red privada virtual) multiplataforma. Es compatible con sistemas operativos Microsoft Windows, GNU/Linux, macOS e incluso tiene aplicaciones gratuitas para Android y iOS.


## Google cloud

Google Cloud (Nube de Google) es una plataforma que ha reunido todas las aplicaciones de desarrollo web que Google estaba ofreciendo por separado. 

## VirtualBox

VirtualBox es una aplicación que sirve para hacer máquinas virtuales con instalaciones de sistemas operativos. Esto quiere decir que si tienes un ordenador con Windows, GNU/Linux o incluso macOS, puedes crear una máquina virtual con cualquier otro sistema operativo para utilizarlo dentro del que estés usando.

#### Servicios de dominio de Active Directory Windows Server 2012

1.	El servidor W2012 debe disponer de una dirección IP fija (estática) y no establecida por DHCP.
2.	Para instalar el rol o característica de Servicios de dominio de Active Directory el servidor W2012 requerirá del rol «Servidor DNS» instalado. Para instalarlo (si aún no lo hemos hecho) pulsaremos la tecla «Windows» del teclado o la combinación de teclas Control + Escape, en el menú de Inicio metro pulsaremos en «Administrador del servidor»:

Pulsaremos en el menú «Administrar» y seleccionaremos «Agregar roles y características»:

Marcaremos el rol «Servidor DNS»:


#### Instalar rol de Servicios de dominio de Active Directory en Windows Server 2012

En nuestro caso este servidor será el primero del dominio, por lo que al agregar el rol de Servicios de dominio de Active Directory se creará el dominio indicado y este servidor será controlador principal de dominio con el catálogo global.

Para instalar el rol de Servicios de dominio de Active Directory en W2012 pulsaremos el botón «Inicio» (o la combinación de teclas Control + Escape), en el menú Inicio pulsaremos en «Administrador del servidor»:

En el Administrador del servidor pulsaremos en «Agregar roles y características»:

Pulsaremos «Siguiente»:



•	Instalación basada en características o en roles: para configurar un solo servidor, agregue roles, servicios de rol y características.
•	Instalación de Servicios de Escritorio remoto: instale los servicios de rol necesarios para que la infraestructura de escritorio virtual (VDI) cree una implementación de escritorio basada en máquinas o en sesiones.

Marcaremos «Seleccionar un servidor del grupo de servidores», seleccionaremos el servidor SRVAJPDSOFT (el servidor que corresponda) , pulsaremos «Siguiente»:

Marcaremos «Servicios de dominio de Active Directory»:


El rol de «Servicios de dominio de Active Directory» requiere de otras características, por lo que si no están instaladas nos lo indicará en la ventana de agregar características requeridas para Servicios de dominio de Active Directory, estas características son «Herramientas de AD DS y AD LDS», «Módulo de Active Directory para Windows PowerShell». Marcaremos «Incluir herramientas de administración (si es aplicable)» y pulsaremos «Agregar características»:

Tras marcar «Servicios de dominio de Active Directory» y sus características requeridas pulsaremos «Siguiente»:

El Asistente para agregar roles y características nos mostrará todos los roles y características elegidas para la instalación, pulsaremos «Instalar»:


A continuación podremos elegir la ubicación (unidad y carpeta) donde se guardará la base de datos, los archivos de registro y la carpeta SYSVOL, por defecto:

    La carpeta de la base de datos: C:/Windows/NTDS
    La carpeta de archivos de registro: C:/Windows/NTDS
    La carpeta SYSVOL: C:/Windows/SYSVOL

El script de Windows PowerShell para implementación de AD DS será:

##### Script de Windows PowerShell para implementación de AD DS

    Import-Module ADDSDeployment
    Install-ADDSForest 
    -CreateDnsDelegation:$false 
    -DatabasePath «C:/Windows/NTDS» 
    -DomainMode "Win2012" 
    -DomainName «proyectoa.local.com» 
    -DomainNetbiosName "AJPDSOFT" 
    -ForestMode «Win2012» 
    -InstallDns:$true 
    -LogPath «C:/Windows/NTDS» 
    -NoRebootOnCompletion:$false 
    -SysvolPath «C:/Windows/SYSVOL» `
    -Force:$true


#### Añadir unidad organizativa y usuario en Active Directory en servidor con Windows Server 2012

Tras instalar el rol de Servicios de dominio de Active Directory podremos crear todos los objetos necesarios para nuestro dominio (impresoras, carpetas compartidas, usuarios, unidades organizativas, alias, grupos, contactos, equipos). Para crear una unidad organizativa pulsaremos la tecla «Windows» del teclado (o las teclas Control + Escape), en el menú de Inicio pulsaremos en «Usuarios y equipos de Active Directory»:
En el árbol de la izquierda pulsaremos con el botón derecho del ratón sobre el servidor «proyectoa.local.com», en el menú desplegable pulsaremos en «Nuevo» – «Unidad organizativa»:
Introduciremos un nombre para la unidad organizativa, por ejemplo «uoDesarrollo» y pulsaremos «Aceptar»:

![imagen](https://user-images.githubusercontent.com/38385565/137443180-ec81de9d-906e-4808-b1bb-da34e8e7219f.png)


Las unidades organizativas servirán como contenedor para otros objetos de Active Directory como usuarios, equipos, impresoras, … También servirán para establecer directivas diferentes por unidad organizativa.
Para agregar un nuevo usuario al dominio Active Directory pulsaremos con el botón derecho del ratón sobre la unidad organizativa en la que queramos crearlo, seleccionaremos «Nuevo» – «Usuario»:


![imagen](https://user-images.githubusercontent.com/38385565/137443218-b14ae541-41dd-408b-99a6-b9829d8580cf.png)

Introduciremos los datos para el usuario (nombre, iniciales, apellidos, nombre completo, nick o nombre de inicio de sesión):


![imagen](https://user-images.githubusercontent.com/38385565/137443242-2f7e4928-1c5f-47bf-8696-09560851dd7b.png)


Introduciremos la contraseña para el nuevo usuario, estableceremos las opciones para la contraseña y pulsaremos «Siguiente»:

![imagen](https://user-images.githubusercontent.com/38385565/137443266-16965ceb-a813-4242-aea3-b374fa15973a.png)

#### Instalacion de servicio DNS

ya configurada la tarjeta de red, se procede a instalar el servicio DNS

![imagen](https://user-images.githubusercontent.com/38385565/137606167-460568b0-5039-4569-b7d1-f85112e610ee.png)


Administrar->Agregar roles y características.
Pulsamos en siguiente y seleccionamos “Instalación basada en características o en roles”.

rol -> Servidor DNS

![imagen](https://user-images.githubusercontent.com/38385565/137606188-d8364309-24b7-479d-94c8-bf1844f31a7c.png)


en la ventana clic en Agregar Características

seleccionamos “Reiniciar automáticamente el servidor de destino en caso necesario”.

![imagen](https://user-images.githubusercontent.com/38385565/137606205-f0babb24-abba-4183-b2a3-5b8f3532c18e.png)

instalar el servicio 

![imagen](https://user-images.githubusercontent.com/38385565/137606213-17112fcf-aebc-4e64-9139-12752175dd68.png)

en panel de administrador
Inicio->Herramientas Administrativas, Administrador del servidor.

![imagen](https://user-images.githubusercontent.com/38385565/137606246-f0303ea6-1f99-4320-a4b7-d2707c1a0d18.png)

#### Equipo a dominio 

Para agregar la computadora a un dominio, es necesario conocer esta información:

    El nombre de dominio
    Un nombre de cuenta de usuario que está registrado en el directorio activo asociado con el servidor
    Versión de Windows Enterprise, Pro o educación

Obtenemos la dirección IP automáticamente, pero asignamos el Servidor DNS preferido de forma manual.

![imagen](https://user-images.githubusercontent.com/38385565/137612770-a7538ee7-078e-4089-a757-217fac67e5e2.png)


Después de completar los datos, debemos comprobar la conexion para ello abrimos una ventana de comandos y hacemos un ping al Servidor.

También comprobaremos que la configuración DNS del cliente es correcta y que el servidor DNS del controlador de dominio está funcionando adecuadamente.

#### LikeWise Open: instalación y configuración de Active Directory en Linux

Likewise Open es una aplicación MIT que te puede ayudar a la gestión de un AD desde tu distribución GNU/Linux. Likewise simplifica lo necesario para configurar y autenticar una máquina Linux dentro de un dominio Active Directory.

Para instalar el paquete likewise-open 

    sudo apt-get install likewise-open
    
En distros Ubuntu más nuevas, utilizar el browser y descargar el paquete DEB:

    http://archive.ubuntu.com/ubuntu/pool/main/l/likewise-open/likewise-open_6.1.0.406-0ubuntu5_amd64.deb

ejecutar el comando
    
    sudo dpkg -i likewise-open_6.1.0.406-0ubuntu5_amd64.deb

la configuración para que funcione en la red se procede a ejecutar en el terminal el siguiente comando:


    sudo domainjoin-cli join nombre-de-mi-dominio.es Administrador

Sutituir nombre-de-mi-dominio.es por el dominio que estes usando según tu caso y Admnistrador por el nombre de la cuenta de administrador que sea o del usuario que necesitemos.

    
Ahora, una vez inicias, podrías usar una tty o también hacerlo desde el menú de login que aparece justo durante el arranque del entorno de escritorio. Introducir el nombre o administrador que has configurado anteriormente de este modo:

    nombre_usuario@mi-nombre-de-dominio.es
 
Y también escribirás la contraseña que dicho usuario o administrador tenga dentro del Active Directory. Tras pulsar el botón para inicio de sesión ya estaremos dentro, pudiendo gestionar lo que necesitemos…


#### Instalacion de FreeBsd 

Menu de bienvenida del sistema operativo.

![imagen](https://user-images.githubusercontent.com/38385565/137670188-aa855cf4-73bc-4722-b9ee-9813b363eeac.png)

seleccionamos la opcion de instalar

![imagen](https://user-images.githubusercontent.com/38385565/137670926-17088035-2a60-41ab-830d-a7bc52a04835.png)

seleccionar el tipo de teclado que manejaremos con s.o.

![imagen](https://user-images.githubusercontent.com/38385565/137672080-9d61622a-f4cc-4e3d-86b5-ad8033a49f67.png)

colocamos nombre para la maquina

![imagen](https://user-images.githubusercontent.com/38385565/137670945-0b3ecfb7-a43e-4bd4-a218-7802d7a2e2f3.png)

configuramos el adaptador de internet

![imagen](https://user-images.githubusercontent.com/38385565/137672179-5a6d4585-02a5-47a1-bd84-2f0fdbb3c266.png)

configuramos IPv4

![imagen](https://user-images.githubusercontent.com/38385565/137672201-73281bc2-9783-43e5-addf-6e88959c4e9a.png)

para el modo de participacion del disco seleccionamos automatico

![imagen](https://user-images.githubusercontent.com/38385565/137672306-1dba0511-5b7c-4804-807f-5f5ba8576092.png)

procedemos con la instalacion 

![imagen](https://user-images.githubusercontent.com/38385565/137672890-7268c74d-60e0-45ac-b1b6-d70026d2959d.png)

seleccionamos el comportamiento del conjunto de discos duros para la maquina virtual bastara el primero

![imagen](https://user-images.githubusercontent.com/38385565/137672935-bb202bc3-aae0-4d69-8e20-18cd593c1086.png)

![imagen](https://user-images.githubusercontent.com/38385565/137673061-eface36b-0b4c-418a-8aa3-89776daf0e63.png)

establecemos contraseña para usuario root

![imagen](https://user-images.githubusercontent.com/38385565/137673091-f523c7d6-eb73-44f2-9cbf-bb8ce03b83ea.png)

![imagen](https://user-images.githubusercontent.com/38385565/137673141-b6ffb236-c556-4f44-8eb1-0d3ec45a8d55.png)


![imagen](https://user-images.githubusercontent.com/38385565/137673157-5c1e9238-d058-40c4-9459-24b633934839.png)


posterior al inicio de sesion ejecutamos los siguiente comandos para instalar gnome 

    freebsd-update install

    pkg install nano
    
    pkg install sudo
    
  ![imagen](https://user-images.githubusercontent.com/38385565/137673482-c75811ce-4d08-4aad-89a1-b1e8229f8834.png)

    pkg install gnome-desktop gdm xorg gnome3 
  
![imagen](https://user-images.githubusercontent.com/38385565/137673509-82fd60db-db3d-4825-ab70-2d90fea4bff9.png)

![imagen](https://user-images.githubusercontent.com/38385565/137673537-14bac301-367c-4af3-a488-28aa01b55c0c.png)

    nano /etc/rc.conf

agregamos estas lineas 

![imagen](https://user-images.githubusercontent.com/38385565/137673583-92601ff2-6a44-4120-9fb1-2cdfce53eae2.png)

    nano /etc/fstab

![imagen](https://user-images.githubusercontent.com/38385565/137673598-751bcf96-8e35-4566-9db2-f5d8a9963bfe.png)


    reboot








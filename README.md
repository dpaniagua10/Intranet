# Intranet
**Proyecto II** 

###### Mario Field     7690 17 20612
###### Daniel Paniagua 7690 17 6640



## Openvpn

OpenVPN es un cliente/servidor VPN (red privada virtual) multiplataforma. Es compatible con sistemas operativos Microsoft Windows, GNU/Linux, macOS e incluso tiene aplicaciones gratuitas para Android y iOS.


## Google cloud

Google Cloud (Nube de Google) es una plataforma que ha reunido todas las aplicaciones de desarrollo web que Google estaba ofreciendo por separado. 


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

![imagen](https://user-images.githubusercontent.com/38385565/137612406-633d86aa-ccb4-42d3-83d9-9960419253c6.png)

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



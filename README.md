# Intranet
**Proyecto II** 


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


# Intranet
**Proyecto Final** 

###### Mario Field     7690 17 20612
###### Daniel Paniagua 7690 17 6640


**Contenido**


1. [Openvpn](#id1)
2. [Google Cloud](#id2)
3. [Virtualbox](#id3)
4. [VMware Workstation Player](#id4)
5. [Servicios de dominio de Active Directory Windows Server 2012](#id5)
6. [Firewall Fortigate Maquina Virtual](#id6)
7. [Politicas Firewall](#id7)
8. [Instalacion de FreeBSD](#id8)
9. [AWS](#id9)






## Openvpn<a name="id1"></a>

OpenVPN es un cliente/servidor VPN (red privada virtual) multiplataforma. Es compatible con sistemas operativos Microsoft Windows, GNU/Linux, macOS e incluso tiene aplicaciones gratuitas para Android y iOS.


## Google cloud<a name="id2"></a>

Google Cloud (Nube de Google) es una plataforma que ha reunido todas las aplicaciones de desarrollo web que Google estaba ofreciendo por separado. 

## VirtualBox<a name="id3"></a>

VirtualBox es una aplicación que sirve para hacer máquinas virtuales con instalaciones de sistemas operativos. Esto quiere decir que si tienes un ordenador con Windows, GNU/Linux o incluso macOS, puedes crear una máquina virtual con cualquier otro sistema operativo para utilizarlo dentro del que estés usando.

## VMware Workstation Player<a name="id4"></a>

(antes conocido como Player Pro) es una aplicación para la virtualización de escritorios que está disponible de forma gratuita para uso personal. Es una herramienta ideal para ejecutar una máquina virtual en un PC con Windows o Linux. 

#### Servicios de dominio de Active Directory Windows Server 2012<a name="id5"></a>

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


#### Firewall Fortigate Maquina Virtual<a name="id6"></a>

Fortinet nos permite descargar y utilizar la máquina virtual de forma gratuita durante dos semanas . Significa que no tiene que comprar nada para probar algunas funciones en su VM.

Lo primero que debe hacer es ir a support.fortinet.com y crear una cuenta gratuita.

Extraiga el archivo descargado y haga doble clic en el archivo de la máquina virtual.

Esto abrirá la ventana Importar máquina virtual donde deberá especificar la ubicación de la nueva máquina virtual:

![imagen](https://user-images.githubusercontent.com/38385565/140584107-4dcd14f6-0702-4a78-adf2-0519110b8f25.png)

Ahora puede iniciar la VM y acceder a la consola CLI. El nombre de usuario predeterminado es admin y la contraseña está en blanco. En el primer inicio de sesión, se le pedirá que establezca la nueva contraseña. A continuación se muestra la captura de pantalla con el proceso de inicio de sesión inicial.

![imagen](https://user-images.githubusercontent.com/38385565/140584153-7cd2e528-c4b7-464b-b0ff-e014fed00174.png)

De forma predeterminada, todos los adaptadores de red de la máquina virtual están en modo puente, esto significa que una de las interfaces obtendrá una dirección IP de su enrutador (servidor DHCP), que proporciona acceso a Internet a su computadora. Una vez que sepa la dirección IP de Fortigate-VM, puede iniciar sesión en su interfaz web. Si tuvo un error relacionado con la licencia, mencionado anteriormente, verá la siguiente página:

![imagen](https://user-images.githubusercontent.com/38385565/140584829-d822eb9c-0dd2-47ce-a1c5-133bf5ff1dbd.png)


Este error tiene algo que ver con la sincronización horaria. La forma más fácil de hacer que funcione es simplemente realizar un restablecimiento de fábrica de Fortigate-VM. El comando se ejecuta el restablecimiento de fábrica .

![imagen](https://user-images.githubusercontent.com/38385565/140584852-28a02a1b-b435-4c5a-8e0b-bcf9da4f94ce.png)

Después del proceso de restablecimiento, deberá volver a iniciar sesión con las credenciales predeterminadas ( administrador y contraseña en blanco). Proporcione la nueva contraseña y busque la dirección IP de la interfaz como se describió anteriormente. Ahora podrá acceder a la GUI y comenzar a configurar el dispositivo.



![imagen](https://user-images.githubusercontent.com/38385565/140585179-245d2801-3a72-431e-82fe-a6b45cfc36ef.png)

#### Politicas Firewall<a name="id7"></a>

###### ruta estatica para navegacion de firewall y red lan

se debe de configurar un gateway por el cual nuestro firewall perimitral tendra acceso a internet por medio de este a traves de politica brindaremos navegacion y acceso de red a los equipos conectados a la red Lan y DMZ.

![imagen](https://user-images.githubusercontent.com/38385565/140585170-4c8d3b7e-f534-4518-a8e4-ced5c12009d1.png)

Dashboard 

monitorio de red

![imagen](https://user-images.githubusercontent.com/38385565/140597640-ce538130-22f7-4e0d-8ee1-cebe06090c72.png)




#### Instalacion de FreeBsd<a name="id8"></a> 

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




### aws<a name="id8"></a>

#### servidor openvpn

dentro del menu principal de servicio aws, seleccionamos ec2

![imagen](https://user-images.githubusercontent.com/38385565/137832610-575a9d80-3170-48ba-bcf7-30278c2394be.png)

luego seleccionamos lanzar instancia

![imagen](https://user-images.githubusercontent.com/38385565/137832694-ff7c0b1d-8770-4855-ad44-2c070e14f684.png)

luego elegimos marketplace, luego buscamos openvpn, elegimos la primera opcion que es el servicio gratuito y luego seleccionar

![imagen](https://user-images.githubusercontent.com/38385565/137832805-63841510-f979-412c-b86f-5877dba92a64.png)

luego continuar 

![imagen](https://user-images.githubusercontent.com/38385565/137832913-220dcb09-4ebd-4a49-a876-93033779bf4a.png)

seleccionamos el de la capa gratuida, luego revisar y lanzar

![imagen](https://user-images.githubusercontent.com/38385565/137832964-785b1017-a2b9-4506-8e58-56eccc351cbf.png)

confirmamos lanzar

![imagen](https://user-images.githubusercontent.com/38385565/137833141-2a3ee416-a1a7-4282-804d-37ee8cba2375.png)

en la ventana creamos el nuevo par de claves, le colocamos un nombre y descarga

posterior a esto ya podemos lanzar la instancia

![imagen](https://user-images.githubusercontent.com/38385565/137833215-cf7e6fb6-9687-44ea-9214-6d37e3cc9f85.png)

nos confirmara

![imagen](https://user-images.githubusercontent.com/38385565/137833317-d82e8ba2-0b0f-4e5d-8671-46c28b4eca72.png)


para conectar seleccionamos los datos para conexion ssh

![imagen](https://user-images.githubusercontent.com/38385565/137833399-23180cc9-c8df-4cca-9c75-69955aba5936.png)

usando el powershell, utilizamos el comando y el archivo de llaves

![imagen](https://user-images.githubusercontent.com/38385565/137833461-8bbbc5da-05be-4666-b945-a5a5bdafdd24.png)


escribimos yes 

![imagen](https://user-images.githubusercontent.com/38385565/137833539-6b620d53-7955-4218-a4d1-c1c26602fdfd.png)


y en los demas unicamente enter

![imagen](https://user-images.githubusercontent.com/38385565/137833600-df928651-d227-4f1e-a674-073043901197.png)

utilizando el comando 

    sudo passwd openvpn

para cambiar la contraseña 

![imagen](https://user-images.githubusercontent.com/38385565/137833627-2528d4d6-cb00-45f7-9e2d-be38a1a03b2d.png)

en la direccion publica que nos brinda el servidor

    ip_publica:943/admin/
    
 ingresamos la contraseña que creamos y la contraseña
 
![imagen](https://user-images.githubusercontent.com/38385565/137833982-f532a0d3-9b46-444d-9d82-74afd7f9c544.png)

seleccionamos configuration -> vpn settings
colocamos como esta en la imagen para activar el trafico hacia internet por medio de la vpn, guardamos los cambios y reiniciamos el servidor

![imagen](https://user-images.githubusercontent.com/38385565/137834116-e955ce0d-3108-451c-b721-d6ff7dec71f4.png)

en la direccion 
    
    ip_publica:943/

usamos el mismo usuario y contraseña para descargar la aplicacion para conectarse como cliente

![imagen](https://user-images.githubusercontent.com/38385565/137834270-30a216b7-5b7d-481c-af93-a1f12f23487a.png)


instalamos e iniciamos, este archivo ya trae la configuracion unicamente colocamos usuario y contraseña

![imagen](https://user-images.githubusercontent.com/38385565/137834391-448864e1-02e2-49a3-aff7-679997dbbfee.png)

![imagen](https://user-images.githubusercontent.com/38385565/137834427-7e7c8131-fa4b-4f87-9e36-ff0b900d9bdf.png)






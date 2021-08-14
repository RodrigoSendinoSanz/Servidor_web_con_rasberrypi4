# Servidor_web_con_rasberrypi4
<img src="https://github.com/RodrigoSendinoSanz/Servidor_web_con_rasberrypi4/blob/main/img/Purple%20Sky%20Profile%20Header.jpg" alt="cabecera">
 Tutorial de como crear un servidor web desde tu casa solo con una rasberry

- Contenido:
     - [MONTAJE](#MONTAJE)
     - [Instalar-el-sistema-operativo:](#Instalar-el-sistema-operativo:)
     - [CREAR-SSH](#CREAR-SSH)
     - [Comandos](#Comandos)
     - [Conexión-remota](#Conexión-remota)
     - [CREACIÓN-DEL-SERVIDOR-WEB](#CREACIÓN-DEL-SERVIDOR-WEB)
     - [ESQUEMA-SERVIDOR](#ESQUEMA-SERVIDOR)  

¿Qué es una raspberry pi?

Es un mini ordenador, del tamaño de una tarjeta de crédito de bajo coste y gran versatilidad

Compra:
https://acortar.link/205RMX
  
Hay varios modelos yo usare el Raspberry Pi 4 Modelo B

## MONTAJE:

Nos encontraremos con los siguientes elementos en nuestro pedido:

<img src="https://github.com/RodrigoSendinoSanz/Servidor_web_con_rasberrypi4/blob/main/img/1.png" alt="cabecera">

Instalar el ventilador:

<img src="https://github.com/RodrigoSendinoSanz/Servidor_web_con_rasberrypi4/blob/main/img/2.png" alt="cabecera">

Tarjeta SD en esta se instala el sistema operativo para ello utilizaremos nuestro usb de adaptador de tarjeta

## Instalar-el-sistema-operativo:
Conectar la tarjeta microSD al ordenador mediante el conector usb insertando la tarjeta como en la imagen:

Ir a : https://www.raspberrypi.org/software/

se descargara un archivo .exe, lo tendrás que ejecutar te pide privilegios de administrador, y efectuar la instalación

elegiremos el sistema en este caso Raspberry PI OS 32 bit (el botón choose OS) y elegiremos la tarjeta sd (choose storage) y le daremos a write

Colocar la tarjeta en la parte trasera inferior de la placa como en la imagen:

Ahora tendrás que conectar un mouse y un teclado en los puertos usb, junto a un cable de ethernet (el amarillo) si es posible, y tambien conectar el cable hdmi en un lateral y en una pantalla y por ultimo conectar el cable de alimentación (conector micro usb)cuya entrada se encuentra al lado del puerto hdmi.

una vez realizado se pulsa en el botón (la primera vez tarda un poco se paciente (y no olvide poner el canal hdmi correcto)) cuando se inicia se aprecian unas luces dentro de la placa base la luz roja es señal de que tiene corriente.

Saldrá una pantalla negra, no te asustes se está iniciando el sistema operativo y espera hasta que aparezca el escritorio en la pantalla que aparece "welcome to raspberry pi" daremos a next para realizar las configuraciones correspondientes, importante recordar la contraseña!, luego conéctese a su red wifi en el siguiente paso

En el siguiente paso se actualizará el software, descargando actualizaciones cuando se actualiza se reinicia.

  

(para apagar el ordenador menú superior icono opción shutdown -> shutdown)

  
  

## CREAR-SSH

> **!!!!!Importante**

Conectamos la tarjeta sd a el ordenador(ventana continuar sin examinar) vamos a la carpeta boot (la principal) en windows: shift y click derecho abrir ventana de powershell aquí 
y escribir : **type nul > ssh** (si nul con una l) nos muestra error pero nos crea el archivo

  
  

### Comandos:

Para abrir una terminal: ctrl+alt+t /f4 (abre la terminal en la carpeta actual) o icono de terminal:

	sudo apt-get update
	sudo apt-get upgrade (Te pregunta si deseas continuar escribe S e intro)(tarda un poco)
	clear limpia la terminal
	pwd muestra en la carpeta en la que te encuentras
	ls lista todas las carpetas que hay en la carpeta donde te encuentras
	cd .. ir hacia atrás en las carpetas en la que te encuentras en: home/pi cd .. /home (cd change directory)
	cd [nombre del directorio] entra al directorio
	mkdir [nombre de carpeta] crea una carpeta
	rmdir [nombre de la carpeta] borra una carpeta
	rm -rf [nombre de la carpeta] borra la carpeta aunque haya contenido dentro
	touch [nombre del archivo] crea un archivo
	rm [nombre del archivo] borra un archivo (rm remove)
	nano [nombre del archivo] abre el editor de texto
	cat [nombre y extensión del archivo] muestra su contenido
	rm -r [archivos] borrar archivo
	rm [fichero] borrar fichero
	cp [origen] [destino]: copia los ficheros de un directorio a otro
	su para entrar en superusuario
	history muestra los comandos que se han escrito
	ifconfig muestra información de ips máscara de subred etc
	sudo apt/get install fetch screen
	screenfetch muestra información del sistema

  

## Conexión-remota:

En una terminal escribe ifconfig en el apartado eth0: obtiene la ip en el apartado inet (debajo de flags=....) tendra esta forma **192.168.1.34**

También se puede utilizar nmap para saber los dispositivos conectador a la red local https://nmap.org/download.html

Una vez instalado pulsar windows +r escribir cmd,escribir: **nmap -sn 192.168.1.0/24** escanea dispostivos conectados a la red pero si solo quieres la información de las ips nmap: **-sn 192.168.1.0/24 -oG -**

Tambien se puede ejecutar **nmap 192.168.1.0/24** mostrando una información más completa

Ahora descargaremos putty https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html y lo instalamos,
e iniciamos, ponemos en el host name la dirección ip de la raspberry,(192.168.1.34) aceptas la ventana, y en login as pones pi y la contraseña es la que pusiste en la configuración del sistema
una vez dentro ejecutar **screenfetch** para asegurarnos de que estamos conectados a la raspberry

comando de configuración: **sudo raspi-config** aquí podremos cambiar la contraseña entre otras

en esta ventana iremos a interfacing options -> y activamos la conexión **SSH** y la **VNC** (para la conexión grafica de manera remota)

instalar 2 programas: **sudo apt-get install -y realvnc-vnc-server realvnc-vnc-view** + enter
 ( permiten mostrar la interfaz gráfica de manera remota)

escribir **vncserver** + enter crea un puerto: 192.168.1.34:1

  

Descargar realvnc https://www.realvnc.com/es/connect/download/viewer/windows/ e instalamos e iniciamos el vncviewer,aceptamos el mensaje de bienvenida y le damos a archivo, nueva conexión en el apartado vncserver escribimos el la ip con el puerto creado **192.168.1.34:1** y en nombre se rellena con el nombre que desees y aceptar le damos doble click al icono de ordenador que se ha creado y nos pide el usuario y la contraseña los cuales son pi y la contraseña que se puso en la configuración


# CREACIÓN-DEL-SERVIDOR-WEB

  
Requisitos:
vnc viewer / putty
usuario y contraseña

  

### RESUMEN

pagina: my.noip.com
sudo apt-get install -y dnsutils
nslookup rodrigosendinosanz.ddns.net
networkctl status
entrar en el router mediante la ip del gateway y crear un dns dinámico
sudo apt-get update
sudo apt-get install apache2
ls /var/www/html/ (para comprobar que se encuentra el index.html)
sudo nano /var/www/html/index.html

  
  

## ESQUEMA-SERVIDOR

### 1) CREAR Y CONFIGURAR NUESTRO NOMBRE DDNS

• https://www.noip.com/

◦ Dynamic DNS

◦ Create Hostname

◦ rodrigosendinosanz

  
  

### 2) COMPROBAR LA RESOLUCIÓN DE NOMBRES DDNS

• Comprobar que tenemos Internet

◦ networkctl status

• nslookup rodrigosendinosanz.ddns.net

• clear

  

### 3) CONFIGURAR EL ROUTER/EQUIPO PARA QUE SE ACTUALICE

  

• Configuración del servidor de nombres dinámicos(DynDNS)

  

### 4) INSTALAR APACHE

• sudo apt-get update

• sudo apt-get install apache2

  

### 5) CONFIGURAR NUESTRA PÁGINA WEB

• ls /var/www/html/

• sudo nano /var/www/html/index.html

  
  

### 6) CONFIGURAR EL ROUTER

• Configurar la tabla NAT del Router

• Configurar el Firewall

◦ Verificar que el puerto 80 no está bloqueado

• Comprobar puertos de entradas

◦ ss -ltpan

sudo apt-get install nmap

◦ nmap rodrigosendinosanz.ddns.net -p 80

  

ir al router y abrir el puerto 80 en la sección de puertos y poner la ip del servidor

  

meter los archivos en la carpeta **var/www/html**
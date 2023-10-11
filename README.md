# @nachoodubra ArchLinux 2023
# ArchLinux
instalacion de arch linux (manual y automatico)

# Modo automatico
# bueno, la problematica aqui, es como instalar arch linux de manera facil
# (obviamente, si quieren romperse la cabeza, podemos hacer la instalacion manual)

# que es arch linux? 
esta distribucion de GNU/linux es la mas liviana y la mas personalizable de todas las distribuciones,
se trata de un linux base, sin controladores ni interfaz grafica, con la capacidad de poder ponerle lo que a uno se le plazca.
es muy buena opcion para los locos que tienen una pc con pocos requisitos (ya que sin interfaz grafica, solo consume 160mb de RAM).
es libre y gratuita, se puede hacer lo que se quiera. aunque, su instalacion es tediosa.


# instalamos Arch Linux de forma automatica
lo primero que debemos hacer, es crear una unidad usb booteable para poder iniciar en este sistema por medio de la ram e instalarlo en nuestra pc
podremos usar rufus, o tambien ventoy... (yo uso ventoy, con solo poner la ISO en el pendrive, ya se puede bootear).
luego de tener la unidad usb, procedemos a bootear la iso..

### placa WIFI
una vez cargue el entorno basico de arch, vamos a proceder a iniciar la placa de red.
### aviso!!!, si tenes la pc conectada por cable, lo mas provable es que ya tengas conexion.

para arrancar la placa wifi, vamos a meter un par de comandos...

# buscar la placa de red
<pre>
ip link
</pre>
con esto vamos a ver como arch llama la placa de red de nuestra pc.
la placa de red, normalmente es la segunda de la lista, en mi caso es wlan0 por ejemplo.

## encendemos la placa
<pre>
ip link set "wlan0 (obvio, esto cambienlo por su placa)" up
</pre>

si en este paso les sale un error, algo asi
### rfkill....

bueno, en ese caso vamos a tener que desbloquear la placa de red metiendo este otro comando.
<pre>
rfkill unblock wifi
</pre>

y ahora, nuevamente usamos el ip link para activarla.

### bueno, ahora vamos a conectarnos a nuestra red.
para ello, vamos a proceder a tipear esto:
<pre>
iwctl
</pre>

con esto, iniciara un servicio para ayudarnos a conectar el internet.

luego vamos a poner
<pre>
device list
</pre>
y vamos a ver como se nombra nuestra placa de red (normalmente station).
luego de eso vamos a escanear las redes y vamos a ver las redes para identificar la nuestra

<pre>
station wlan0 scan
station wlan0 get-networks
</pre> 

### aclaremos que estos codigos deben adaptarlos a su pc, no todas las pc son iguales

y bueno ahora para conectarnos a la red vamos a pedirle lo siguiente:
<pre>
station wlan0 connect "el nombre de tu red wifi"
</pre>

al darle enter, nos pedira la contraseña de nuestra red, la cual colocamos y damos enter.
listo, ahora ya estamos conectados a internet de manera inalambrica, para corroborar que funciona la red, vamos a salir de iwctl y ponemos:
<pre>
ping www.google.com
</pre>
si aparecen mediciones en ms, es porque estamos recibiendo señal del servidor de google, lo cual, tenemos internet... 
si esto no pasa, volve a intentar con iwctl, suele pasar de que no se conecte.


# instalar usando Archinstall
una vez que tenemos el wifi configurado, a lo que vamos a proceder, es a iniciar un comando para ayudarnos y no rompernos la cabeza instalando arch.
estando en el inicio de arch, luego del wifi, vamos a tipear:
<pre>
archinstall
</pre>

y vamos a encontrarnos con una interfaz guiada para instalar arch en nuestra pc.

## lenguaje del instalador: (recomiendo dejarlo en ingles).
## mirrors (son los que despues nos ayudaran a instalar paquetes, se marcan con la tecla espacio, recomiendo si sos de argentina, que uses el de arg y el brasileño).
## keyboard (con esto vamos a configurar el teclado(en argentina se usa la-latin1), pero solo para arch, no para el entorno grafico, si instalar hyprland, tengo un repositorio aparte donde esplico como dejarlo bien).
## drive(s) (aca vamos a decirle en que disco queremos instalar arch, lo buscan y lo marcan con la tecla espacio(acuerdense que esto borrara todos sus datos en ese disco)).
## bootloader (bueno aca es complicado, si tienen UEFI, solo dejenlo como esta, y para hacer un dual boot con windows, arch debe instalarse manualmente).
## swap (esta es la memoria de intercambio entre el SO y el disco, para que la ram no se llene, yo no uso, por motivo de mejorar el rendimiento del ssd, pero se puede usar igual).
## hostname (aca por defecto dice "archlinux", pero podemos poner el nombre que nosotros queramos, es para crear el usuario root).
## root passwd (con esta contraseña, entraremos al root de nuestro dispositivo, acuerdense tanto el hostname y esta contraseña.).
## user account (estos son los usuarios del pc, debes crear uno (yo le puse el nombre y la contraseña igual a las anteriores (root) para no confundirme)).
## profile (aqui vamos a decirle a arch que es lo que queremos, si queremos una instalacion minima o con entornos graficos(yo elegi entorno grafico hyprland, que es un buen gestor de ventanas, pero pueden elegir lo que quieran)).
## select audio (aqui vamos a poner el driver de audio, si tu pc es media nueva, usa "pipewire", sino, "pulseaudio").
## kernels (esto recomiendo que no lo toquen, es el kernel de linux).
## additional packages (no agreguen nada, instalen paquetes luego de que termine la instalacion de arch).
## additional repositories (lo mismo que los packages).
## configure network (pongan en este como en la ISO de instalacion, asi les instala los modulos de wifi).
## timezone (aca elegis la zona horaria tuya (en mi caso arg)).

luego de configurar todo esto, dale install nomas y a esperar.


## primer inicio
bueno, si en la parte de profile, elegiste sddm como iniciador de sesion, vamos a proceder a iniciar el servicio:

para ello, iniciamos el pc y debemos colocar el hostname y luego la contraseña para arranca como superusuario
luego vamos a proceder a poner este comando:
<pre>
systemctl enable sddm
systemctl start sddm
</pre>

### reiniciamos el pc y ya nos deberia iniciar con el iniciador de seccion.

dependiendo el entorno que hallas elegido, va a iniciar en cada entorno.
si quieres configurar hyprland y que quede bastante lindo e intuitivo, [metete aqui](https://github.com/Dubranachoo/hyprland/)

# @nachoodubra ArchLinux 2023


Semana 10
===========
Esta semana comenzaremos con la segunda parte del curso enfocada en la construcción de aplicaciones para 
sistemas embebidos, especificamente Internet de la cosas.

Objetivos
----------
1. Introducir algunos conceptos básicos de sistemas embebidos.
2. Configurar las herramientas de desarrollo.

Configuración del entorno de desarrollo
----------------------------------------
Durante esta semana trabajaremos con este 
`material introductorio <https://drive.google.com/open?id=1rxlrmvW4SUUDyVw-T9Z2PrEkh6xBReHaqsedfFkezzo>`__.

El material anterior cubre los pasos necesarios para instalar y configurar el entorno de desarrollo de software bajo el 
el framework de arduino. En este escenario se utilizan los lenguajes C y C++. En la siguiente sección se abordarán los 
pasos para configurar un entorno desarrollo utilizanzo python, específicamente `micropython <https://micropython.org/>`__.

Micropython: macOS x (High Sierra, 10.13.6)
---------------------------------------------
Los siguientes pasos asumen que el usuario no tiene privilegios de administración y que el driver serial de la interfaz 
USB presente en la tarjeta de desarrollo de la plataforma ESP8266 ha sido previamente instalado y configurado.

* Abra la terminal serial

* Descargue la aplicación ``pip`` así ::

    curl https://bootstrap.pypa.io/get-pip.py -o ~/Downloads/get-pip.py

* Si la aplicación ``curl`` no está disponible, descargue la aplicación 
  `pip <https://bootstrap.pypa.io/get-pip.py>`__ (click derecho salvar) en la carpeta  ~/Downloads/

* Una vez descargada cambie de directorio ::

    cd ~/Downloads/

* Ejecute :: 

    python ~/Downloads/get-pip.py --user

* Adicione ``pip`` al ``PATH`` ::

    nano ~/.bash_profile

* Edite el archivo ``.bash_profile`` con la siguiente línea ::

    export PATH=$PATH:~/Library/Python/2.7/bin

* Presiona ``ctrl + x``, luego la letra ``y`` y por último ``ENTER``.

* Cierre todas las instancias abiertas de la terminal.

* Abra la terminal y escriba ::

    echo $PATH

* Verifique que la siguiente ruta aparezca (``username`` será el nombre de usuario de la sesión actual) ::

    /Users/<username>/Library/Python/2.7/bin

* Instale la herramienta ``esptool`` ::

    pip install --user esptool

* Instale la herramienta ``adafruit ampy`` ::

    pip install --user adafruit-ampy

* Descargue la `imagen de micropython <http://micropython.org/resources/firmware/esp8266-20180511-v1.9.4.bin>`__ al 
  directorio ~/Downloads/

* Cambie al directorio ~/Downloads/

* Borre la memoria de programa del ESP8266 ::

    esptool.py --port /dev/tty.SLAB_USBtoUART erase_flash

* Almacene en la memoria de programa del ESP8266 la imagen de micropython::

    esptool.py --port /dev/tty.SLAB_USBtoUART --baud 460800 write_flash --flash_size=detect -fm dio 0 esp8266-20180511-v1.9.4.bin

* Ejecute el siguiente comando y verifique que el resultado sea ``boot.py`` ::

    ampy --port /dev/tty.SLAB_USBtoUART ls

* Finalmente abra un emulador de terminal serial y verifique que la interfaz REPL de micropython funciona::

    screen /dev/tty.SLAB_USBtoUART 115200

* Presione un par de veces la tecla ``ENTER``. Debe aparecer el prompt del REPL: ``>>>``

Una vez finalizados con éxito los pasos anteriores, estamos listos para comenzar.

Micropython: en windows
------------------------

* Instale python (puede ser la versión 3.7)

* Abra la línea de comandos de windows

* Instale ``esptool``:: 
    
    pip install esptool

* instale adafruit ampy ::

    pip install adafruit-ampy

* Descargue la `imagen de micropython <http://micropython.org/resources/firmware/esp8266-20180511-v1.9.4.bin>`__ al 
  directorio Descargas.

* Cambie al directorio Descargas.

* Conecte la tarjeta del ESP8266 e instale los `drivers <https://www.silabs.com/documents/public/software/CP210x_Universal_Windows_Driver.zip>`__.

* Verifique el puerto COM asignado por el sistema operativo:

    .. image:: ../_static/Com.jpeg
       :scale: 80%

* Borre la memoria de programa del ESP8266. Cambie COM? por el puerto apropiado ::

    esptool.py --port COM? erase_flash

* Almacene en la memoria de programa del ESP8266 la imagen de micropython::

    esptool.py --port COM? --baud 460800 write_flash --flash_size=detect -fm dio 0 esp8266-20180511-v1.9.4.bin

* Ejecute el siguiente comando y verifique que el resultado sea ``boot.py`` ::

    ampy --port COM? ls

* Descargue la aplicación `putty <https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html>`__. Configure el puerto serial y
  salve la sesión:

    .. image:: ../_static/putty.jpeg
       :scale: 80%

* Abra la terminal y presione ``ENTER`` un par de veces. Debe aparecer el ``prompt`` del ``REPL``

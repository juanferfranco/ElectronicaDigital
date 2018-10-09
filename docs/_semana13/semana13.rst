Semana 13
===========
Esta semana terminaremos el último ejercicio de la semana 11 relacionado con la intergración de sensores y actuaodres 
utilizando buses digitales. Introduciremos también el uso del radio WiFi que posee el ESP8266. Este radio permitirá 
conectarnos a internet.

Objetivos
----------
1. Introducir el uso de sensores con buses digitales para ampliar las posibilidades del ESP8266.
2. Conectarnos a internet mediante el uso del radio WiFi del ESP8266.

Ejercicio: sensores con buses digitales
----------------------------------------
Para este ejercicio vamos a utilizar un sensor de temperatura, humedad y presión barométrica. El sensor es fabricado por 
la empresa Bosh y la referencia es `BME280 <https://www.bosch-sensortec.com/bst/products/all_products/bme280>`__. Este 
sensor utiliza un bus digital llamado ``I2C``. Este bus permite comunicar la tarjeta ESP8266 con el sensor por medio dos 
cables llamados SCL (para el reloj) y SDA (para los datos).

Antes de conectar el sensor al ESP8266, desconecte el cable USB para remover la alimentación. Debemos conectar el sensor así:

========== =======
ESP8266    BME280
========== =======
3.3V       VCC
GND        GND
GPIO5(D1)  SCL       
GPIO4(D2)  SDA     
========== =======

En cuanto al software, debemos instalar una biblioteca que permita leer el sensor. Siga los siguientes pasos para instalar
la biblioteca:

* Ingrese al menún Programa.
* Seleccione Incluir Librería.
* Seleccione Gestionar Librería.
* En el campo de filtrado de búsqueda escriba BME280 ``Adafruit BME280``.
* Seleccione el item encontrado e instale la biblioteca.
* Decargue esta `biblioteca <https://github.com/adafruit/Adafruit_Sensor>`__. Click en  Clone or Download y luego
  en download ZIP.
* Una vez descargada la biblioteca seleccione en el IDE de Arduino Programa, Incluir Libraría, Añadir Libraría .zip ...

Siga los siguientes pasos para probar el sensor:

* Abra Archivo, Ejemplos. Navegue hasta la parte inferior de los ejemplos colocando el mouse sobre la flecha negra que está 
  en la parte inferior del menú.
* Seleccione Adafruit BME280 Library y luego bme280test
* En la función ``setup()`` modifique ``Serial.begin(9600);`` por ``Serial.begin(115200);`` y ``status = bme.begin();`` 
  por ``status = bme.begin(0x76);``
* Compile y grabe el programa.
* Abra el Monitor Serie asegurándose que la velocidad de comunicación es 115200.
* El resultado esperado será::

    Temperature = 27.14 *C
    Pressure = 843.77 hPa
    Approx. Altitude = 1517.64 m
    Humidity = 55.11 %

Ejercicios: 
-----------------
En `esta guía de trabajo <https://drive.google.com/open?id=1O6BrQznhc4xFkr81Uo4WUVgL-0lndwY4i_cG2qArKZs>`__ vamos a 
realizar ejercicios que nos permitirán: 

* Conectar el ESP8266 a internet
* Interactuar con servicios web en servidores http
* Enviar notificaciones
* Realizar comunicación machine to machine empleando TCP/IP. 
Semana 15
===========
Durante esta semana haremos dos ejercicios. Primero, vamos a enviar a un servidor en internet los valores de varios sensores. Segundo, 
vamos controlar de manera remota un actuador.

Objetivos
----------
1. Enviar información de un sensor a un servidor en internet.
2. Modificar de manera remota el estado de un actuador.

Ejercicios
-----------
Los siguientes ejercicios vamos a realizarlos utilizando la plataforma Adafruit IO. La comunicación entre el ESP8266 y el servicio de 
Adafruit IO la ralizaremos utilizando TCP/IP y el protocolo MQTT. El primer paso para entender los ejercicios es leer la información 
de `este enlace <https://learn.adafruit.com/mqtt-adafruit-io-and-you/overview>`__.

¿Cuáles son los problemas de HTTP (REST)?
¿Qué ventajas tiene MQTT sobre HTTP (REST)?
¿Qué es un Broker MQTT?
¿Cuál es la función del Broker MQTT?

Ejercicio: crear una cuenta en Adafruit IO
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Ingrese al siguiente `sitio <https://io.adafruit.com>`__ y cree una cuenta en el MQTT Broker de Adafruit.

Tome nota de su nombre de usuario de cuenta y su clave o KEY. Dicha clave será utilizada por todos sus dispositivos para autenticarse con 
Adafruit IO.

¿Qué es un Feed? ¿Para qué sirve?

¿Puedo utilizar MQTT para acceder al historial de un feed?

Ejercicio: creación de feeds
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Cree un feed para cada una de las variables: temperatura, humedad, presión barométrica, pulsador.
Cree un feed llamdo onoff para controlar remotamente una salida digital que visulizaremos mediante un LED.

Ejercicio: creación de un dashboard
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Para los feeds temperatura, humedad y presión barométrica cree gauges.
Para el pulsador creen un indicador luminoso.
Para el control onoff cree un suiche deslizante.

Ejercicio: instale la biblioteca MQTT
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Utilice el gestor de bibliotecas de arduino, como en la práctica realizada para el sensor BME280, para 
instalar la biblioteca Adafruit MQTT. Esta biblioteca le permitirá al ESP8266 hablar el protocolo MQTT.

Ejercicio: pruebe la comunicación
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Cargue el ejemplo MQTT_ESP8266. No olvide configurar: la red WiFi, su nombre de usuario y KEY. Modifique el feed photocell
por alguno de los correspondientes con temperatura, humedad, presión barométrica o pulsador. Verifique que el feed onoff
es igual al que usted creó (nombre 100% idéntico). En MQTT los dispositivos se suscriben al feed que les interesa y publican al feed 
que desean actualizar. 

No olvide abrir el dashboard para verificar el funcionamieto de la aplicación.

Ejercicio: sensores y actuador MQTT
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Modifque el ejemplo anterior considerando todos los feeds creados.

Ejercicio: QoS
^^^^^^^^^^^^^^^
¿Qué es la calidad del servicio en MQTT? ¿Cuándo podría ser importante?

Ejercicio: conecte Adafruit io a IFTTT
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Verifique el siguiente `proyecto <https://learn.adafruit.com/using-ifttt-with-adafruit-io/overview>`__ que ilustra cómo conectar 
IFTTT con adafruit io.



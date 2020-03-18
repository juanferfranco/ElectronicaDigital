Semana 9
===========
Esta semana comenzaremos con la segunda parte del curso enfocada en la construcción de aplicaciones para 
sistemas embebidos, uno de los pilares del internet de las cosas.

Objetivos
----------
1. Introducir algunos conceptos básicos de sistemas embebidos.
2. Configurar las herramientas de desarrollo.
3. Realizar los primeros ejercicios de programación del sistema embebido.


Sesión 1
---------

Configuración del entorno de desarrollo
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Durante esta semana trabajaremos con este 
`material introductorio <https://docs.google.com/presentation/d/1A663TX543Dh2V4xkvaiVQ8RLKFTkC3CALfXTRrJiWsE/edit?usp=sharing>`__.

El material anterior cubre los pasos necesarios para instalar y configurar el entorno de desarrollo de software bajo el 
el framework de arduino. En este escenario se utilizan los lenguajes C y C++.


Sesión 2
---------
En esta sesión vamos a cubrir parte del material que nos quedó faltando de la sesión anterior. Así como ver
si han podido poner a funcionar cada uno de ustedes su tarjeta. Adicionalmente, vamos a realizar algunos ejercicios
básicos de programación.


Ejercicio 1: flujo de trabajo 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
El flujo de trabajo para realizar aplicaciones con arduino será:

* Crear un archivo nuevo. Este archivo inicia con dos funciones: ``setup()`` y ``loop()``.
* La función setup se ejecuta solo una vez al momentos de energizar el ESP32 o cuando se presiona el botón de reset.
* La función loop será llamada constantemente por el framework de arduino.
* Una vez escrita la parte de la aplicación que se desea probar, se debe compilar. El proceso de compilación verifica que 
  el programa no tenga errores sintácticos y genera el código de máquina que posteriormente se cargará en la memoria de
  programa del ESP32. Para realizar la verificación y compilación se selecciona el primer ícono en la parte superior izquierda.
* Una vez compilada la aplicación se procede a grabar la memoria del microcontrolador. Esto se realiza con el segundo ícono
  de la parte superior izquierda.
* Finalmente se selecciona el ícono del monitor serial en la esquina superior derecha. Este ícono permite abrir la terminal
  serial por medio la cual se podrán visualizar los mensajes que el ESP32 le enviará al computador utilizando el 
  objeto ``Serial``.

Vamos a probar todos los pasos anteriores con este programa:

.. code-block:: cpp
   :lineno-start: 1

    void setup() {
      Serial.begin(115200);
    }

    void loop() {
      Serial.print("Hello from ESP32\n");  
      delay(1000);  
    }

Ejercicio 2: API de arduino 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
En `este enlace <https://www.arduino.cc/reference/en/>`__ se pueden consultar muchas de las funciones disponibles para
realizar programas usando el API de Arduino.

El siguiente programa permite encender y apagar un LED conectado a un puerto de entrada salida:

.. code-block:: cpp
   :lineno-start: 1

    void setup()
    {
      pinMode(2, OUTPUT);
    }
    
    void loop()
    {
      digitalWrite(2, HIGH);
      delay(1000); // Wait for 1000 millisecond(s)
      digitalWrite(2, LOW);
      delay(1000); // Wait for 1000 millisecond(s)
    }

El siguiente programa permite leer un puerto digital y encender y apagar un LED:


.. code-block:: cpp
   :lineno-start: 1

    void setup()
    {
      pinMode(2, OUTPUT);
      pinMode(3,INPUT);
      
    }
    
    void loop()
    {
      if(digitalRead(3) == HIGH){
        digitalWrite(2, HIGH);  
      }
      else{
        digitalWrite(2, LOW);
      }
    }

Ejercicio 3: RETO 1
^^^^^^^^^^^^^^^^^^^^
Realice un programa que lea el estado de dos switches y encienda solo
uno de 4 LEDs.

Ejercicio 4: puerto serial
^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: cpp
   :lineno-start: 1

    void setup()
    {
      pinMode(2, OUTPUT);
      pinMode(3,INPUT);
      Serial.begin(115200);
      
    }
    
    void loop()
    {
      if(digitalRead(3) == HIGH){
        digitalWrite(2, HIGH);  
        Serial.println("LED ON");
      }
      else{
        digitalWrite(2, LOW);
        Serial.println("LED OFF");
      }
    }

Ejercicio 5: RETO 2
^^^^^^^^^^^^^^^^^^^^
Modifique el código del reto 1 para indicar por el puerto serial
cuál de los 4 LEDs está encendido.

Ejercicio 6: ADC
^^^^^^^^^^^^^^^^^
El siguiente programa lee una señal análoga y la convierte a digital.

.. code-block:: cpp
   :lineno-start: 1

    void setup()
    {
      pinMode(2, OUTPUT);
      pinMode(3,INPUT);
      Serial.begin(115200);
    }
    
    void loop()
    {
        
        Serial.println(analogRead(A0));
        delay(1000);
    }


Ejercicio 7: RETO 3
^^^^^^^^^^^^^^^^^^^^
Lea el valor de una entrada analógica. Si la entrada es menor
a 340 enciende un led verde y envía por el puerto serial solo una
vez LED_VERDE. Si es mayor a 340 pero menor a 700 enciende solo 
el LED amarillo y envía por el puerto serial solo una vez LED_AMARILLO.
Finalmente, si es mayor a 700 enciende solo el LED rojo y envía por
el puerto serial solo una vez LED_ROJO. Tenga en cuenta que al entrar
a cada rango se debe enviar solo una vez el mensaje por el puerto
serial.

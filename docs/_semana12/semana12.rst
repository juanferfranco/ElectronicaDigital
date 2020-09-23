Semana 12
===========

Unidad 6: Introducción a los sistemas embebidos
------------------------------------------------

Actividades
^^^^^^^^^^^^^

Actividad 1
*************
* Fecha: septiembre 23 de 2020 - 8 a.m.
* Descripción: encuentro sincrónico para trabajar de manera
  grupal en los ejercicios.
* Recursos: ingresa al grupo de Teams.
* Duración de la actividad: 1 hora 40 minutos 
* Forma de trabajo: colaborativo con solución de dudas en tiempo real.

Actividad 2
*************
* Fecha: septiembre 23 a septiembre 25 de 2020.
* Descripción: continuar con los ejercicios
* Recursos: ejercicios propuestos. 
* Duración de la actividad: 5 horas de trabajo autónomo
* Forma de trabajo: individual.

Ejercicio 1: flujo de trabajo 
##################################
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
###############################
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
###############################
Realice un programa que lea el estado de dos switches y encienda solo
uno de 4 LEDs (un LED para cada estado)

Ejercicio 4: puerto serial
###############################
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
###############################
Modifique el código del reto 1 para indicar por el puerto serial
cuál de los 4 LEDs está encendido.

Ejercicio 6: ADC
###############################
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

Actividad 3
*************
* Fecha: septiembre 25 de 2020 - 8 a.m.
* Descripción: solución de dudas de los ejercicios y trabajo en el reto.
* Recursos: ingresa al grupo de Teams.
* Duración de la actividad: 1 hora 40 minutos 
* Forma de trabajo: colaborativo con solución de dudas en tiempo real.

Ejercicio 7: RETO 3
###############################
Lea el valor de una entrada analógica. Si la entrada es menor
a 340 enciende un led verde y envía por el puerto serial solo una
vez LED_VERDE. Si es mayor a 340 pero menor a 700 enciende solo 
el LED amarillo y envía por el puerto serial solo una vez LED_AMARILLO.
Finalmente, si es mayor a 700 enciende solo el LED rojo y envía por
el puerto serial solo una vez LED_ROJO. Tenga en cuenta que al entrar
a cada rango se debe enviar solo una vez el mensaje por el puerto
serial.
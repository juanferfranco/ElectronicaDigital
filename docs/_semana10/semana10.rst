Semana 10
===========

Esta semana continuaremos con la exploración del API de arduino y
algunas características de C/C++.


Ejercicio 1
------------
Hasta ahora hemos explorado varias maneras de interactuar con
dispositivos externos por medio de puertos de entrada salida usando:

* Salidas digitales
* Entradas digitales
* Entradas analógicas

Ahora en este ejercicio vamos a explorar las salida analógicas. Dichas
salidas, en principio son digitales pero moduladas en ancho de pulso
o de PWM. Para ello usamos esta función:

.. code-block:: cpp
   :lineno-start: 1

    analogWrite(pin, value)

Que produce una señal cuadra en pin con un duty cycle dado por value,
como se muestra en la figura de `este <https://www.arduino.cc/en/tutorial/PWM>`__
sitio. 

Analice el siguiente ejemplo:

.. code-block:: cpp
   :lineno-start: 1

    #define ledPin 3
    #define analogPin 0

    uint16_t counter = 0;
    int8_t direction = 1;

    void setup() {
        Serial.begin(115200);
        pinMode(ledPin, OUTPUT);
    }


    void loop() {
        analogWrite(ledPin, counter); 
        counter = (counter + direction);
        if(counter == 0) direction = 1;
        if(counter == 129) direction = -1;

        Serial.println(counter);
        delay(20);

    }

Ejercicio 2: RETO 1
--------------------
Monte un circuito (en tinkercad) y realice un programa que permita controlar
el brillo de un LED mediante un potenciómetro.

Tenga que presente que el valor del potenciómetro va de 0 hasta 5V y este
se convierte a un valor entre 0 y 1023, es decir, la conversión se realiza
en 10 bits.

COnsidere que el valor del PWM puede ir de 0 a 255. Para garantizar que
value estará en ese rango podemos emplear una de las funciones matemáticas
que ofrece el API de arduino:

.. code-block:: cpp
   :lineno-start: 1

    map(value, fromLow, fromHigh, toLow, toHigh)

En este caso map toma fromLow y lo convierte a toLow y
fromHigh y lo convierte a toHigh. Los valores intermedios son mapeados de
manera lineal.

NOTA: para el ESP32 se debe usar una función diferente para el PWM. Ver el
`este <https://techexplorations.com/guides/esp32/begin/pwm/>`__ enlace.

Ejercicio 3:
--------------
Analice el siguiente código:

.. code-block:: cpp
   :lineno-start: 1

    void setup() {
       Serial.begin(115200);

    }


    void loop() {

      uint8_t counter = 20;

      counter++;

      Serial.println(counter);

      delay(100);

    }

Compare el código anterior con este:

.. code-block:: cpp
   :lineno-start: 1

    void setup() {
       Serial.begin(115200);

    }


    void loop() {

      static uint8_t counter = 20;

      counter++;

      Serial.println(counter);

      delay(100);

    }

Ahora compare con este otro código:

.. code-block:: cpp
   :lineno-start: 1

	uint8_t counter = 5;

    void setup() {
       Serial.begin(115200);

    }


    void incCounter() {
      static uint8_t counter = 10;
      counter++;
      Serial.print("Counter in incCounter: ");
      Serial.println(counter);

    }

    void loop() {
      static uint8_t counter = 20;
      counter++;
	    Serial.print("Counter in loop: ");
      Serial.println(counter);
      incCounter();
      Serial.print("Counter outside loop: ");
      Serial.println(::counter);
      ::counter++;
      delay(500);
    }

¿Qué podemos concluir?


Ejercicio 4
------------
Analizar el siguiente ejemplo:

.. code-block:: cpp
   :lineno-start: 1

    const uint8_t ledPin =  3;
    uint8_t ledState = LOW;
    uint32_t previousMillis = 0;
    const uint32_t interval = 1000;

    void setup() {
      // set the digital pin as output:
      pinMode(ledPin, OUTPUT);
    }
    
    void loop() {
      uint32_t currentMillis = millis();
    
      if (currentMillis - previousMillis >= interval) {
        previousMillis = currentMillis;
        if (ledState == LOW) {
          ledState = HIGH;
        } else {
          ledState = LOW;
        }´
    }

Ejercicio 5: RETO 2
--------------------
Realice un programa que encienda y apague tres LEDs a
1 Hz, 5 Hz y 7 Hz respectivamente utilizando la técnica vista en
el ejercicio 4.
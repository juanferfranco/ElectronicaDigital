Semana 13
===========

Unidad 6: Introducción a los sistemas embebidos
------------------------------------------------
Esta semana continuaremos con la exploración del API de arduino y
algunas características de C/C++.


Actividades
^^^^^^^^^^^^^

Actividad 1
*************
* Fecha: septiembre 30 de 2020 - 8 a.m.
* Descripción: encuentro sincrónico para trabajar de manera
  grupal en los ejercicios.
* Recursos: ingresa al grupo de Teams.
* Duración de la actividad: 1 hora 40 minutos 
* Forma de trabajo: colaborativo con solución de dudas en tiempo real.

Ejercicio 1
##############
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

``analogWrite`` produce una señal cuadra con un duty cycle dado por ``value``,
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
########################
Monta un circuito (en tinkercad) y realiza un programa que permita controlar
el brillo de un LED mediante un potenciómetro.

Ten en presente que el valor del potenciómetro va de 0 hasta 5V y este
se convierte a un valor entre 0 y 1023, es decir, la conversión se realiza
en 10 bits.

Considera que el valor del PWM puede ir de 0 a 255. Para garantizar que
``value`` estará en ese rango podemos emplear una de las funciones matemáticas
que ofrece el API de arduino:

.. code-block:: cpp
   :lineno-start: 1

    map(value, fromLow, fromHigh, toLow, toHigh)

En este caso map toma ``fromLow`` y lo convierte a ``toLow`` y
``fromHigh`` y lo convierte a ``toHigh``. Los valores intermedios son mapeados de
manera lineal.

NOTA: para el ESP32 se debe usar una función diferente para el PWM. Ver
`este <https://techexplorations.com/guides/esp32/begin/pwm/>`__ enlace.

Ejercicio 3:
#############
Analiza el siguiente código:

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

Compara el código anterior con este:

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

Ahora compara con este otro código:

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

¿Qué puedes concluir?

Ejercicio 4
#############

Analiza el siguiente ejemplo:

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
        }
    }

¿Qué hace este programa?

Ejercicio 5: RETO 2
######################
Realice un programa que encienda y apague tres LEDs a
1 Hz, 5 Hz y 7 Hz respectivamente utilizando la técnica vista en
el ejercicio 4.

Actividad 2
*************
* Fecha: septiembre 30 a octubre 2 de 2020.
* Descripción: continuar con los ejercicios
* Recursos: ejercicios propuestos. 
* Duración de la actividad: 5 horas de trabajo autónomo
* Forma de trabajo: individual.

En tus horas de trabajo autónomo más explorar algunas
características de los lenguajes. Adicionalmente, veremos
cómo podemos encapsular el código en ``TAREAS`` e introduciremos
el uso de clases. 

Ejercicio 6
#############
Vamos a analizar uno de los ejemplos que vienen con el
SDK de arduino. Este ejemplo nos permite ver cómo podemos
hacer uso de los arreglos para manipular varios LEDs:

.. code-block:: cpp
   :lineno-start: 1    
    
    int timer = 100;           // The higher the number, the slower the timing.
    int ledPins[] = {
      2, 7, 4, 6, 5, 3
    };       // an array of pin numbers to which LEDs are attached
    int pinCount = 6;           // the number of pins (i.e. the length of the array)
    
    void setup() {
      // the array elements are numbered from 0 to (pinCount - 1).
      // use a for loop to initialize each pin as an output:
      for (int thisPin = 0; thisPin < pinCount; thisPin++) {
        pinMode(ledPins[thisPin], OUTPUT);
      }
    }
    
    void loop() {
      // loop from the lowest pin to the highest:
      for (int thisPin = 0; thisPin < pinCount; thisPin++) {
        // turn the pin on:
        digitalWrite(ledPins[thisPin], HIGH);
        delay(timer);
        // turn the pin off:
        digitalWrite(ledPins[thisPin], LOW);
    
      }
    
      // loop from the highest pin to the lowest:
      for (int thisPin = pinCount - 1; thisPin >= 0; thisPin--) {
        // turn the pin on:
        digitalWrite(ledPins[thisPin], HIGH);
        delay(timer);
        // turn the pin off:
        digitalWrite(ledPins[thisPin], LOW);
      }
    }


Ejercicio 7
##############
El siguiente código muestra cómo podemos encapsular completamente
el código del RETO en tareas.

.. code-block:: cpp
   :lineno-start: 1    

    void setup() {
      task1();
      task2();
    }

    void task1(){
      static uint32_t previousMillis = 0;
      static const uint32_t interval = 1250;
      static bool taskInit = false;
      static const uint8_t ledPin =  3;
      static uint8_t ledState = LOW;
      
      if(taskInit == false){
        pinMode(ledPin, OUTPUT);	
        taskInit = true;
      }
      
      uint32_t currentMillis = millis();	
      if ( (currentMillis - previousMillis) >= interval) {
        previousMillis = currentMillis;
        if (ledState == LOW) {
          ledState = HIGH;
        } else {
          ledState = LOW;
        }
        digitalWrite(ledPin, ledState);
      }
    }

    void task2(){
      static uint32_t previousMillis = 0;
      static const uint32_t interval = 370;
      static bool taskInit = false;
      static const uint8_t ledPin =  5;
      static uint8_t ledState = LOW;
      
      if(taskInit == false){
        pinMode(ledPin, OUTPUT);	
        taskInit = true;
      }
      
      uint32_t currentMillis = millis();	
      if ( (currentMillis - previousMillis) >= interval) {
        previousMillis = currentMillis;
        if (ledState == LOW) {
          ledState = HIGH;
        } else {
          ledState = LOW;
        }
        digitalWrite(ledPin, ledState);
      }
    }

    void loop() {
      task1();
      task2();
    }

Una de las ventajas del código anterior es que favorece el trabajo
en equipo. Nota que se puede entregar a cada persona del equipo una
tarea. Finalmente, uno de los miembros del equipo podrá integrar
todas las tareas así:

.. code-block:: cpp
   :lineno-start: 1 

	  void task1(){
    .
    .
    .
    }
    
    void task2(){
    .
    .
    .
    }

    void task3(){
    .
    .
    .
    }

    void setup() {
	    task1();
	    task2();
      task3();
	  }

	  void loop() {
	    task1();
	    task2();
      task3();
	  }


Ejercicio 8
##################

Observa detenidamente el código de ambas tareas. Verás que es muy similar.
En este ejercicio veremos una construcción interesante de
C++ que favorece el reuso de código. Nota que el código de las tareas
1 y 2 es prácticamente el mismo, solo que está actuando sobre diferentes datos. 

¿Cómo así?

Analicemos por partes. Primero, la inicialización de la tarea:

Para la tarea 1 (task1):

.. code-block:: cpp
   :lineno-start: 1 

    if(taskInit == false){
	  	pinMode(ledPin, OUTPUT);	
	    taskInit = true;
	  }

Para la tarea 2 (task2):

.. code-block:: cpp
   :lineno-start: 1 

    if(taskInit == false){
	  	pinMode(ledPin, OUTPUT);	
	    taskInit = true;
	  }


En el código anterior cada tarea tiene una variable que permite
activar el código solo un vez, es decir, cuando taskInit es false.
Esto se hace así para poder inicializar el puerto de salida donde
estará el led conectado. Recuerde que esto se haga solo una vez.
¿Cuándo ocurrirá? Cuando llamemos taskX() (X es 1 o 2) en la función
setup().

Segundo, el código que se llamará repetidamente en la función loop:

Para la tarea 1:

.. code-block:: cpp
   :lineno-start: 1 

	   if ( (currentMillis - previousMillis) >= interval) {
	     previousMillis = currentMillis;
	     if (ledState == LOW) {
	       ledState = HIGH;
	     } else {
	       ledState = LOW;
	     }
	     digitalWrite(ledPin, ledState);
	   }


Para la tarea 2:

.. code-block:: cpp
   :lineno-start: 1 

	  uint32_t currentMillis = millis();	
	   if ( (currentMillis - previousMillis) >= interval) {
	     previousMillis = currentMillis;
	     if (ledState == LOW) {
	       ledState = HIGH;
	     } else {
	       ledState = LOW;
	     }
	     digitalWrite(ledPin, ledState);
	   }

Nota que los datos sobre los que actúa cada código, aunque
tienen el mismo nombre son datos distintos:

Para la tarea 1:

.. code-block:: cpp
   :lineno-start: 1 

	  static uint32_t previousMillis = 0;
	  static const uint32_t interval = 1250;
	  static bool taskInit = false;
	  static const uint8_t ledPin =  3;
	  static uint8_t ledState = LOW;

Para la tarea 2:

.. code-block:: cpp
   :lineno-start: 1 

	  static uint32_t previousMillis = 0;
	  static const uint32_t interval = 370;
	  static bool taskInit = false;
	  static const uint8_t ledPin =  5;
	  static uint8_t ledState = LOW;

Pero ¿Por qué son distintos? porque estamos declarando las variables
como estáticas dentro de cada tarea.
Esto implica que las variables son privadas a cada función pero
viven en memoria como si se tratara de variables globales.

Esto introduce la siguiente pregunta: ¿Qué tal si pudiéramos tener
el mismo código, pero cada vez que lo llamemos indicarle sobre
que datos debe actuar? Pues lo anterior es posible en C++ usando
una construcción conocida como clase.

La clase nos permite definir un nuevo tipo dato y los algoritmos
que se pueden aplicar a ese nuevo tipo de dato. En este caso,
necesitamos que cada tarea pueda tener sus propias variables para
previousMillis, interval, ledPin, ledState.

.. code-block:: cpp
   :lineno-start: 1    

    class LED{
        private:
            uint32_t previousMillis;
            const uint32_t interval;
            const uint8_t ledPin;
            uint8_t ledState = LOW;
	  };

De esta manera en cada tarea podremos crear un nuevo LED así:

.. code-block:: cpp
   :lineno-start: 1

    void task1(){
        static LED led;
    }

.. code-block:: cpp
   :lineno-start: 1

    void task2(){
        static LED led;
    }

A cada nuevo LED se le conoce como un objeto. led es
la variable por medio de las cuales podremos acceder a cada
uno de los objetos creados en task1 y task2.

Notas:

* Cada objeto es independiente, es decir, cada objeto tiene su propia
  copia de cada variable definida en la clase.
  ¿Cuál es el contenido de cada objetos? el contenido es un uint32_t,
  un const uint32_t, un const uint8_t y uint8_t a los cuales les
  hemos dado nombres: previousMillis, interval, ledPin y ledState
  respectivamente.
* Las variables led definidas en task1 y task2 NO SON OBJETOS,
  son variables de tipo LED que permiten acceder al contenido de cada objeto. 
* led es una variable propia de cada tarea.
* Nota que las variables definidas en LED son privadas (private). Esto
  quiere decir que no vamos a acceder a ellas directamente. Ya veremos
  más abajo cómo modificar sus valores.

Nuestro nuevo tipo LED tiene un problema y es que no permite definir para cada
LED creado el intervalo y el puerto donde se conectará. Para resolver lo anterior
se introduce el concepto de constructor de la clase. El constructor,
permite definir los valores iniciales de cada objeto.

.. code-block:: cpp
   :lineno-start: 1    

    class LED{
        private:
            uint32_t previousMillis;
            const uint32_t interval;
            const uint8_t ledPin;
            uint8_t ledState = LOW;

        public:
            LED(uint8_t _ledpin, uint32_t _interval): ledPin(_ledpin), interval(_interval) {
                pinMode(_ledpin, OUTPUT);
                previousMillis = 0;
            }
	  };

El constructor de la clase es un método que recibe los valores
iniciales del objeto y no devuelve nada.

Ahora si podemos definir cada objeto:

.. code-block:: cpp
   :lineno-start: 1

    void task1(){
        static LED led(3,725);
    }

.. code-block:: cpp
   :lineno-start: 1

    void task2(){
        static LED led(5, 1360);

.. code-block:: cpp
   :lineno-start: 1

    class LED{

    private:
      uint32_t previousMillis;
      const uint32_t interval;
      const uint8_t ledPin;
      uint8_t ledState = LOW;

    public:
      LED(uint8_t _ledpin, uint32_t _interval): ledPin(_ledpin), interval(_interval) {
       pinMode(_ledpin, OUTPUT);
       previousMillis = 0;
      }

      void toggleLED(){
       uint32_t currentMillis = millis();	
       if ( (currentMillis - previousMillis) >= interval) {
         previousMillis = currentMillis;
         if (ledState == LOW) {
           ledState = HIGH;
         } else {
           ledState = LOW;
         }
         digitalWrite(ledPin, ledState);
       }
      }
    };   


Finalmente, al llamar toggleLED debemos indicar sobre qué objeto
deberá actuar:

.. code-block:: cpp
   :lineno-start: 1

    void task1(){
        static LED led(3,725);

        led.toggleLED();
    }

.. code-block:: cpp
   :lineno-start: 1

    void task2(){
        static LED led(5, 1360);
        led.toggleLED();
    }

La versión final del código será:

.. code-block:: cpp
   :lineno-start: 1

    class LED{

      private:
        uint32_t previousMillis;
        const uint32_t interval;
        const uint8_t ledPin;
        uint8_t ledState;

      public:
        LED(uint8_t _ledpin, uint32_t _interval): ledPin(_ledpin), interval(_interval) {
          pinMode(_ledpin, OUTPUT);
          previousMillis = 0;
          ledState = LOW;
        }

        void toggleLED(){
          
          uint32_t currentMillis = millis();	
          if ( (currentMillis - previousMillis) >= interval) {
            previousMillis = currentMillis;
            if (ledState == LOW) {
              ledState = HIGH;
            } else {
              ledState = LOW;
            }
            digitalWrite(ledPin, ledState);
          }
        }
    };

	  void task1(){
	    static LED led(3,1250);
	    led.toggleLED();
	  }

	  void task2(){
	    static LED led(5,375);
	    led.toggleLED();
	  }

	  void setup() {
	    task1();
	    task2();
	  }

	  void loop() {
	    task1();
	    task2();
	  }

Ejercicio 9
###############

Podemos llevar un paso más allá el ejercicio anterior si añadimos
el concepto de arreglo. ¿Para qué? Observa que el código de
task1 y task2 es muy similar. Tal vez podamos resolver el problema
usando únicamente una tarea:

.. code-block:: cpp
   :lineno-start: 1    

    class LED{

    private:
      uint32_t previousMillis;
      const uint32_t interval;
      const uint8_t ledPin;
      uint8_t ledState = LOW;

    public:
      LED(uint8_t _ledpin, uint32_t _interval): ledPin(_ledpin), interval(_interval) {
       pinMode(_ledpin, OUTPUT);
       previousMillis = 0;
      }

      void toggleLED(){
       uint32_t currentMillis = millis();	
       if ( (currentMillis - previousMillis) >= interval) {
         previousMillis = currentMillis;
         if (ledState == LOW) {
           ledState = HIGH;
         } else {
           ledState = LOW;
         }
         digitalWrite(ledPin, ledState);
       }
      }

    };

    void setup() {

    }

    void task(){
      static LED leds[2] = {{3,725},{5,1300}};

      for(int i= 0; i < 2; i++){
        leds[i].toggleLED();
      }

    }

    void loop() {
        task();
    }


Ejercicio 10
##############
Ahora vamos a explorar un concepto fundamental en C y C++: los punteros.

¿Qué son los punteros? para entenderlos vamos a dar un salto mortal
en complejidad analizando este ejemplo:

.. code-block:: cpp
   :lineno-start: 1    

    void setup(){
        Serial.begin(115200);
    }


    void processData(uint8_t *pData, uint8_t size, uint8_t *res){
      uint8_t sum = 0;

      for(int i= 0; i< size; i++){
        sum = sum + *(pData+i) - 0x30;
      }
      *res =  sum;
    }

    void loop(void){
      static uint8_t rxData[10];
      static uint8_t dataCounter = 0;  

      if(Serial.available() > 0){
          rxData[dataCounter] = Serial.read();
          dataCounter++;
        if(dataCounter == 5){
           uint8_t result = 0;
           processData(rxData, dataCounter, &result);
           dataCounter = 0;
           Serial.println(result);
        }
      }
    }


Ejercicio 11
##############

En este ejercicio vas a leer cómo funcionan las comunicaciones
seriales. Para ello vamos a tomar material de
`este <https://learn.sparkfun.com/tutorials/serial-communication/all>`__
sitio.


Actividad 3
*************
* Fecha: octubre 2 de 2020 - 8 a.m.
* Descripción: solución de dudas de los ejercicios.
* Recursos: ingresa al grupo de Teams.
* Duración de la actividad: 1 hora 40 minutos 
* Forma de trabajo: colaborativo con solución de dudas en tiempo real.
Semana 11
===========
Esta semana exploraremos una de las características más importantes
de C/C++ y son los llamados punteros. Adicionalmente, veremos
cómo podemos encapsular más el código en una tarea y por medio
de clases. En la segunda sesión de esta semana realizaremos la
evaluación sumativa 3.

Sesión 1
-----------
En esta sesión vamos a abordar los siguientes conceptos:

* Arreglos
* Encapsular nuestro código completamente en tareas.
* Usar el concepto de clase para reusar parte del código.
* Punteros
* Introducción a las comunicaciones seriales.


Ejercicio 1 
^^^^^^^^^^^^^
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


Ejercicio 2
^^^^^^^^^^^^^
El siguiente código muestra cómo podemos encapsular completamente
el código del RETO 2, de la semana pasada, en tareas.

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
en equipo. Note que se puede entregar a cada persona del equipo una
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


Ejercicio 3
^^^^^^^^^^^^^

Observe detenidamente el código de ambas tareas. Verá que es muy similar.
En este ejercicio veremos una construcción interesante de
C++ que favorece el reuso de código. Note que el código de las tareas
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

Note que los datos sobre los que actúa cada código, aunque
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

* las variables led definidas en task1 y task2 NO SON OBJETOS,ç
  son variables de tipo LED que permiten acceder al contenido de cada objeto. 

* led es una variable propia de cada tarea.
* Note que las variables definidas en LED son privadas (private). Esto
  quiere decir que no vamos a acceder a ellas directamente. Ya veremos
  más abajo cómo modificar sus valores.

Nuestro nuevo tipo LED tiene un problema y es que no permite definir para cada
LED creado el intervalo y el puerto donde se conectará.Para ello,
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
            bool taskInit = false;
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
	  task1();
	  task2();
	}

	void task1(){
	  static LED led(3,1250);
	  led.toggleLED();
	}

	void task2(){
	  static LED led(5,375);
	  led.toggleLED();
	}

	void loop() {
	  task1();
	  task2();
	}

Ejercicio 4:
^^^^^^^^^^^^^
Podemos llevar un paso más allá el ejercicio anterior si añadimos
el concepto de arreglo. ¿Para qué? Observe que el código de
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


Ejercicio 5
^^^^^^^^^^^^^
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

Sin embargo, antes de abordar el ejemplo, haremos una parada de unos
minutos para analizar lentamente qué son los punteros.

Ejercicio 6
^^^^^^^^^^^^^
En este ejercicio vamos a introducir cómo funcionan las comunicaciones
seriales. Para ello vamos a tomar material de
`este <https://learn.sparkfun.com/tutorials/serial-communication/all>`__
sitio.

Ejercicio 7: RETO
^^^^^^^^^^^^^^^^^^
El reto de esta semana no será un ejercicio, PERO ES MUY IMPORTANTE.
Se trata de estudiar detalladamente el material introducido en la sesión
1.

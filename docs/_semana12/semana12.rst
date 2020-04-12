Semana 12
===========

Esta semanas vamos a estudiar más en detalle cómo funciona el puerto
serial de un controlador y cómo se usa este desde el framework de arduino.
Vamos a introducir también la técnica de programación
con máquinas de estados.

Sesión 
--------
En esta sesión comenzaremos revisando cómo funciona el puerto serie.

Ejercicio 1
^^^^^^^^^^^^^
En este ejercicio vamos a introducir cómo funcionan las comunicaciones
seriales. Para ello vamos a tomar material de
`este <https://learn.sparkfun.com/tutorials/serial-communication/all>`__
sitio.

Ejercicio 2
^^^^^^^^^^^^^^^^^^
¿Dónde encuentro el API de arduino para el manejo del serial?

`Aquí <https://www.arduino.cc/reference/en/language/functions/communication/serial/>`__

Ejercicio 3
^^^^^^^^^^^^^^^^^^
Vamos a responder algunas preguntas (hay que tomar nota de las soluciones)

* ¿Qué pasa cuando hago un Serial.available()?
* ¿Qué pasa cuando hago un Serial.read()?
* ¿Qué pasa cuando hago un Serial.read() y no hay nada en el buffer de
  recepción?
* Un patrón común al trabajar con el puerto serial es este:

.. code-block:: cpp
   :lineno-start: 1  

    if(Serial.available() > 0){
        int dataRx = Serial.read() 
    }

* ¿Cuánto datos lee Serial.read()?
* ¿Y si quiero leer más de un dato? No olvide que no se pueden leer más datos
  de los disponibles en el buffer de recepción, claramente porque no hay
  más datos que los que tenga allí.

Ejercicio 4
^^^^^^^^^^^^^^^^^^
Vamos a leer 3 datos del puerto serial:

.. code-block:: cpp
   :lineno-start: 1  

    if(Serial.available() >= 3){
        int dataRx1 = Serial.read()
        int dataRx2 = Serial.read() 
        int dataRx3 = Serial.read() 
    }

Ejercicio 5
^^^^^^^^^^^^^^^^^^
¿Qué escenarios podría tener en este caso?

.. code-block:: cpp
   :lineno-start: 1  

    if(Serial.available() >= 2){
        int dataRx1 = Serial.read()
        int dataRx2 = Serial.read() 
        int dataRx3 = Serial.read() 
    }

Explique detalladamente, recurriendo al material del
ejercicio 1, cómo se podría explicar cada escenario.

Ejercicio 6: RETO
^^^^^^^^^^^^^^^^^^
Piense cómo podría hacer lo siguiente:

.. code-block:: cpp
   :lineno-start: 1  

    void taskSerial(){
        // Tener encapsulado en la tarea el buffer
    }

    void loop(){
        taskSerial();
    }


* Almacenar los datos en su propio buffer de recepción
  (el buffer será un arreglo).
* El buffer debe estar encapsulado en la tarea
* Los datos almacenados en el buffer no se pueden perder
  entre llamados a taskSerial() en la función loop.  
* ¿Cómo hacer para saber en cualquier parte de taskSerial()
  cuántos datos tengo guardados en el buffer de recepción?

Ejercicio 7
^^^^^^^^^^^^^^^^^^
Vamos a detenernos un momento en el software del lado del
computador: el terminal. Veamos dos de ellas, la terminal
de arduino y `esta <https://sourceforge.net/projects/scriptcommunicator/>`__
otra (scriptcommunicator)

* ¿Qué es un programa terminal? 
* ¿Para qué sirve?

Ejercicio 8
^^^^^^^^^^^^^^^^^^
Considere el siguiente programa

.. code-block:: cpp
   :lineno-start: 1  

    void setup()
    {
      Serial.begin(9600);
    }

    void loop()
    {

      if(Serial.available() > 0){

        Serial.read();

        int8_t var = -1;

        Serial.println("Inicio de la prueba");
        Serial.write(var);
        Serial.print("\n");
        Serial.print(var);
        Serial.print('\n');
        Serial.println("Fin de la prueba"); 
      }
    }

* Observe el resultado de la prueba.
* ¿Qué observa en la terminal de arduino para cada caso?

.. code-block:: cpp
   :lineno-start: 1  

    Serial.write(var);
    Serial.print(var);


* ¿Qué observa en scriptcommunicator para cada caso?
*  En la siguiente parte del código:

.. code-block:: cpp
   :lineno-start: 1  

    if(Serial.available() > 0){

        Serial.read();

Comente la línea Serial.read()

.. code-block:: cpp
   :lineno-start: 1  

    if(Serial.available() > 0){

        //Serial.read();

* ¿Qué ocurre? ¿Por qué ocurre esto?

En la siguiente parte del código:

.. code-block:: cpp
   :lineno-start: 1  

    Serial.println("Inicio de la prueba");
    Serial.write(var);
    Serial.print("\n");
    Serial.print(var);
    Serial.print('\n');
    Serial.println("Fin de la prueba"); 

¿Cuál es la diferencia entre estas dos líneas de código?

.. code-block:: cpp
   :lineno-start: 1  

   Serial.print("\n");

   Serial.print('\n');

Ejercicio 9: RETO
^^^^^^^^^^^^^^^^^^
Considere el siguiente código para analizar en scriptcommunicator:

.. code-block:: cpp
   :lineno-start: 1  

    void setup()
    {
      Serial.begin(9600);
    }

    void loop()
    {

      if(Serial.available() > 0){
        Serial.read();
        int8_t var = 255;
        int8_t var2 = 0xFF;

        Serial.write(var);
        Serial.print(var);
        Serial.write(var2);
        Serial.print(var2);

      }
    }

Explique con convicción qué está ocurriendo en cada caso.

Ejercicio 10: RETO
^^^^^^^^^^^^^^^^^^^
Este reto es para las horas de trabajo autónomas del curso:

* Repita lentamente los ejercicios de esta sesión: analice, analice,
  analice.
* Experimente con los ejercicios de esta sesión y de nuevo: analice;
  haga cambios; hágase preguntas antes de ejecutar los cambios; si no
  compila busque por qué, si no encuentra la respuesta documente y
  consulte a su profe; antes de ejecutar un cambio piense qué pasará y
  luego ejecute, compare, analice.
* Haga lo anterior con cada ejercicio hasta que se asegure de comprender.
  NO OLVIDE: antes de ejecutar es importante predecir qué pasará y luego
  contrastar.

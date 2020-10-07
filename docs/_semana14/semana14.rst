Semana 14
===========

Unidad 7: comunicaciones seriales
----------------------------------
Ahora que ya conoces cómo hacer operaciones de entrada
salida básicas con el microcontrolador, vamos a profundizar
un poco más en las comunicaciones seriales.

Actividades
^^^^^^^^^^^^^

Actividad 1
*************
* Fecha:octubre 7 de 2020 - 8 a.m.
* Descripción: encuentro sincrónico para trabajar de manera
  grupal en los ejercicios.
* Recursos: ingresa al grupo de Teams.
* Duración de la actividad: 1 hora 40 minutos 
* Forma de trabajo: colaborativo con solución de dudas en tiempo real.

Ejercicio 1
##############
En este ejercicio vamos a introducir cómo funcionan las comunicaciones
seriales. Para ello vamos a tomar material de
`este <https://learn.sparkfun.com/tutorials/serial-communication/all>`__
sitio.

Ejercicio 2
##############
¿Dónde encuentro el API de arduino para el manejo del serial?

`Aquí <https://www.arduino.cc/reference/en/language/functions/communication/serial/>`__

Ejercicio 3
##############
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
* Pero profe, yo quiero leer 4 datos. Entonces ¿Qué modificación debes hacerle
  al código anterior?

Ejercicio 4
##############
Vamos a leer 3 datos del puerto serial:

.. code-block:: cpp
   :lineno-start: 1  

    if(Serial.available() >= 3){
        int dataRx1 = Serial.read()
        int dataRx2 = Serial.read() 
        int dataRx3 = Serial.read() 
    }

Ejercicio 5
##############
¿Qué escenarios podrías tener en este caso?

.. code-block:: cpp
   :lineno-start: 1  

    if(Serial.available() >= 2){
        int dataRx1 = Serial.read()
        int dataRx2 = Serial.read() 
        int dataRx3 = Serial.read() 
    }

Explica detalladamente recurriendo al material del
ejercicio 1, cómo se podría explicar cada escenario.

Ejercicio 6: RETO
####################
Piensa cómo podrías hacer lo siguiente:

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
  ¿Qué me invento para ir contando cuántos datos tengo almacenados?

Ejercicio 7
####################
Vamos a detenernos un momento en el software del lado del
computador: el terminal. Veamos dos de ellas, la terminal
de arduino y `esta <https://sourceforge.net/projects/scriptcommunicator/>`__
otra (scriptcommunicator)

* ¿Qué es un programa terminal? 
* ¿Para qué sirve?

Ejercicio 8
####################
Considera el siguiente programa

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

* Observa el resultado de la prueba.
* ¿Qué ves en la terminal de arduino para cada caso?
* ¿Qué ves en scriptcommunicator para cada caso?

Ahora observa este par de líneas de código del código
anterior

.. code-block:: cpp
   :lineno-start: 1  

    Serial.write(var);
    Serial.print(var);


* ¿Qué observas en scriptcommunicator para cada caso?
* ¿Por qué?

En la siguiente parte del código:

.. code-block:: cpp
   :lineno-start: 1  

    if(Serial.available() > 0){

        Serial.read();

Comenta la línea Serial.read()

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

Ejercicio 9: MINI- RETO
#########################
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

Actividad 2
*************
* Fecha: octubre 7 a octubre 9 de 2020.
* Descripción: continuar con los ejercicios
* Recursos: ejercicios propuestos. 
* Duración de la actividad: 5 horas de trabajo autónomo
* Forma de trabajo: individual.

Termina los ejercicios anteriores.

Ejercicio 10: RETO
######################

Este es un mini-RETO para que INVESTIGUES!!!


* Repite lentamente los ejercicios 1 al 9: analiza, analiza,
  analiza.
* Experimente con los ejercicios y de nuevo analice;
  realiza cambios; formula preguntas antes de ejecutar los cambios; si no
  compila busca por qué, si no encuentras la respuesta documenta y
  consulta al profe; antes de ejecutar un cambio piensa qué pasará y
  luego ejecuta, compara, analiza.
* Haga lo anterior con cada ejercicio hasta que se asegure de comprender.
  NO OLVIDE: antes de ejecutar es importante predecir qué pasará y luego
  contrastar.

Actividad 3
*************
* Fecha: octubre 9 de 2020 - 8 a.m.
* Descripción: evaluación.
* Recursos: ingresa al grupo de Teams.
* Duración de la actividad: 1 hora 40 minutos 
* Forma de trabajo: colaborativo con solución de dudas en tiempo real.

Es esta sesión vamos realizar una evaluación que involucra lo aprendido en
las últimas semanas.
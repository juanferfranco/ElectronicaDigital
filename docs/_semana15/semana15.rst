Semana 15
===========

Unidad 8: máquinas de estado
----------------------------------
En esta última unidad del curso vamos a abordar
una técnica de construcción de software para el microcontrolador
que permitirá hacer un uso eficiente de la CPU y adicionalmente
poder realizar varias tareas de manera concurrente.

Actividades
^^^^^^^^^^^^^

Actividad 1
*************
* Fecha:octubre 14 de 2020 - 8 a.m.
* Descripción: encuentro sincrónico para trabajar de manera
  grupal en los ejercicios.
* Recursos: ingresa al grupo de Teams.
* Duración de la actividad: 1 hora 40 minutos 
* Forma de trabajo: colaborativo con solución de dudas en tiempo real.


Ejercicio 1: enunciado del problema
#####################################

En un proyecto interactivo se requiere conectar un controlador a una
aplicación interactiva (AI). 

Considere:

* Para simular la AI utilice scriptcommunicator. Esto se requiere porque debemos 
  transmitir bytes NO caracteres ASCII. Ojo!
* La AI siempre iniciará la comunicación.
* La secuencia de bytes más grande será de 20 bytes.

PASOS para realizar la comunicación:

1. La AI inicia una transacción enviando el byte 3E.
2. El controlador deberá responder con el byte 4A.
3. La AI no podrá continuar hasta no recibir la respuesta del controlador.
   Una vez el controlador responda, la AI enviará al controlador
   un paquete de bytes así:

.. code-block:: cpp
   :lineno-start: 1

    Byte 1 : longitud
    Byte 2 : Dirección
    Byte 3 : Comando
    Byte 4 a n : Datos
    Byte n+1: verificacion

* El byte de longitud, es el primer byte de la trama e indica cuántos bytes la AI
  enviará a continuación, es decirm de byte 2 hasta el byte n + 1.
* La AI calculará el byte de verificación así: Byte1 XOR Byte2 XOR … XOR ByteN.
* En C la operación XOR se realiza utilizando el operador 

.. code-block:: cpp
   :lineno-start: 1

   ^

4. El controlador esperará hasta un 1 segundo a que la trama llegue. Si esta condición
  NO se cumple el controlador enviará a la AI el byte 3D. La AI deberá inciar de
  nuevo la secuencia de comunicación desde el paso 1. 
  
  Una vez el controlador tenga la trama completa calculará el byte de cerificación
  de la misma manera que la AI lo hizo. El resultado debe ser igual al bytes de verificación
  recibido. Sí el byte de verificación calculado no corresponde al byte de verificación
  recibido, el controlador enviará el byte 3F y la AI deberá reenviar la trama. 
  Sí hay coincidencia el controlador deberá responder a la AI con el byte 4A y luego enviar
  la siguiente secuencia de bytes:

.. code-block:: cpp
   :lineno-start: 1

    Byte 1 : longitud
    Byte 2 : Byte4 recibido
    Byte m : Byten recibido
    Byte m+1 : verificación

5. Sí la AI recibe correctamente el paquete deberá responder con el byte 4A. 
   El controlador quedará preparado para volver al paso 1, es decir, esperar por una nueva
   trama. Sí ha pasado 1 segundo y el controlador no recibe el 4A, entonces deberá
   retransmitir el paquete a la AI. Este comportamiento solo se detendrá hasta que la
   AI envie el 4A.


Actividad 2
*************
* Fecha: octubre 14 a octubre 16 de 2020.
* Descripción: continuar con los ejercicios
* Recursos: ejercicios propuestos. 
* Duración de la actividad: 5 horas de trabajo autónomo
* Forma de trabajo: individual.

Actividad 3
*************
* Fecha: octubre 16 de 2020 - 8 a.m.
* Descripción: solución de dudas de los ejercicios.
* Recursos: ingresa al grupo de Teams.
* Duración de la actividad: 1 hora 40 minutos 
* Forma de trabajo: colaborativo con solución de dudas en tiempo real.
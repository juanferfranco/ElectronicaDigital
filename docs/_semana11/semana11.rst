Semana 11
===========
Esta semana aprenderemos a utilizar las diferentes alternativas de entrada/salida que provee micropython con el 
ESP8266. Adicionalmente seguiremos un flujo de trabajo de aplicaciones (workflow) similar al utilizado en otras plataformas 
como Arduino.

Objetivos
----------
1. Seguir un flujo de trabajo para desarrollar aplicaciones.
2. Explorar las capacidades de entrada/salida de la plataforma.


Ejercicios de python utilizando micropython
--------------------------------------------
* Abra la interfaz de REPL de micropython. Utilice putty en windows o screen en macosX.
* Cree algunas variables e inicialice dichas varibles con valores.
* ¿Por qué no puede utilizar las siguientes palabras como nombres de variables::

    and         for         raise
    assert      from        return
    break       global      try
    class       if          while
    continue    import      with
    def         in          yield
    del         is
    elif        lambda
    else        not
    except      or
    exec        pass
    finally     print
* En python es posible escribir comentarios en el código utilizando ``#`` al inicio de la línea; sin embargo,
  cuando escribamos programas evitaremos emplear los comentarios ya que a diferencia de un computador, esta información
  ocupará espacio en la memoria de programa del controlador.
* Recuerde que python no emplea, como otros lenguajes de programación, llaves (``{ }``) para formar bloques de código. 
  En cambio, utiliza identación. Utilizando la interfaz REPL, evalue el siguiente código:

  .. code-block:: python

     if sum == 10:
        print('Es igual')
     else:
        print('Es diferente')

* Cree los siguientes tipos de datos: numérico, cadena, lista, tupla y diccionario. 
* Cree los siguiente tipos de datos numéricos: enteros, números en hexadecimal, número en punto
  flotante, números complejos. (¿Qué se puede concluir de los número complejos en micropython?)
* Cree la siguiente cadena: mi_nombre= 'Juan Franco'. ¿Cuál es el resultado de las siguientes expresiones?

  .. code-block:: python

     s = mi_nombre[0]     
     s = mi_nombre[2:4]    
     s = mi_nombre[1:4]    
     s = mi_nombre[3:]    

* ¿Cuál es el resultado de hacer mi_nombre*2?
* ¿Cuál es el resultado de hacer mi_nombre + 'UPB'
* Cuál es el resultado de hacer 

  .. code-block:: python

     s = 'Hola'
     s[0] = R
     
* Cree una lista. Cambie uno de los valores de la lista. ¿Qué puede concluir de las listas en relación a las cadenas?
* Cree una matriz de 3x3 utilizando una lista.
* Para los siguientes ejercicios asuma ``A = 0 0 1 1 1 1 0 0`` , ``B = 1 1 0 0 1 1 0 1``
* Haga ejemplos que utilicen los siguientes operandos: ``+,-,*,/,%,**``
* Haga ejemplos que utilicen los siguientes operandos: ``==, !=, >,<, >=, <=``
* Haga ejemplos que utilicen los siguientes operandos: ``and, or, not``
* Haga ejemplos que utilicen los siguientes operandos: ``=, +=, -=, *=, /=, **=``
* Para este ejercicio, repase las operaciones a nivel de bits que realizamos en la primer parte del curso. 
  Luego haga ejemplos que utilicen los siguientes operandos: ``&, |, ^, ~, <<, >>``
* Realice un ejemplo para cada una de las siguientes estructuras de control:
  
  .. code-block:: python

     if
     if..else
     elif
     for
     while
     break
     continue
     pass

* Utilice la interfaz REPL y explore las siguientes funciones:

  .. code-block:: python

     int()
     float()
     abs()
     bin()
     ceil()
     exp()
     floor()
     hex()
     log()
     pow()
     round()
     sqrt()

* En algunas cadenas, es necesario utilizar caracteres ASCII no imprimibles por ejemplo: ``\n`` (newline), 
  ``\r`` (carriage-return), ``\t`` (tab). Experimente en la terminal REPL con estos caractares.
* En python es posible utilizar cadenas formateadas. Experimente con las siguientes líneas de código:

  .. code-block:: python

     '{} {}'.format(1, 2)
     '{1} {0}'.format('one', 'two')
* Experimente con las siguientes funciones para manejo de cadenas:

  .. code-block:: python

     count()
     find()
     len()
     isalpha()
     isalnum()
     isdigit()
     islower()
     iupper()
     lower()
     upper()
     lstrip()
     rstrip()
* Experimente con las siguientes funciones para manejo de listas:

  .. code-block:: python

     del()
     list.append()
     cmp()
     len()
     max()
     Min()
     list.count()
     list.index()
     list.insert()
     list.remove()
     list.reverse()
     list.sort()

* Experimente con las siguientes funciones para manejo de diccionarios:

  .. code-block:: python

     cmp()  
     len
     del()
     d.clear()
     d.keys()
     d.values()

* Experimente con las siguientes funciones para manejo de fechas y tiempo. Note que será necesario que importe la biblioteca
  time (import time)

  .. code-block:: python

     time.localtime()
     time.sleep()
     time.sleep_ms()
     time.sleep_us()

* Realice una función que multiplique dos números recibidos como parámetros.
* Tenga presente que las variables que utilice en una función serán variables locales a la función. Por tanto, una vez 
  la función retorne, la información de las variables locales se perderá. Explique el comportamiento de este programa:

  .. code-block:: python

    def foo():
        y = "local"
    foo()
    print(y)



* Explique qué pasa al ejecutar este código y por qué:

  .. code-block:: python

    x = "global"
    def foo():
        x = x * 2
        print(x)
    foo()

* Para utilizar variables locales y globales, considere el siguiente ejemplo:

  .. code-block:: python

     x = "global"
     def foo():
         global x
         y = "local"
         x = x * 2
         print(x)
         print(y)
        
     foo()
     
* Analice el siguiente programa:

  .. code-block::python

     x = 5
     def foo():
         x = 10
         print("local x:", x)

     foo()
     print("global x:", x)

* En micropython es posible leer información desde la terminal. Analice el siguiente código:

  .. code-block::python

     name = input('Ingrese su nombre: ')
     print(name)

* Es posible manipular archivo un micropython; sin embargo, es recomendable evitar, por ahora, el uso de archivos a menos 
  que se indique lo contrario. La razón es que un mal uso de estos puede dejar inservible la memoria del microcontrolador.
  Como ejemplo, para listar el contenido del sistema de archivos de micropython ejecute este programa:

  .. code-block:: python

     import os 
     os.listdir()

Ejercicio: Flujo de trabajo
----------------------------
Con micropython se puede seguir un flujo de trabajo similar al utilizado con el framework de Arduino para realizar 
aplicaciones. Para ello, necesitaremos la aplicaciones instalada la semana pasada: ``ampy``. La aplicación ampy será 
ejecutada desde una línea de comandos en windows o una terminal en macosX.

* Abra la terminal de comandos y ejecute::

    ampy --help

* Antes de utilizar la herramienta ampy, utilice el RPEL para deshabilitar la salida de depuración de micropython::

  >>>import esp
  >>>esp.osdebug(None)

* Con ampy es posible escribir código en el computador y correr ese código en el ESP8266. Para ecribir código se recomieda 
  utilizar un editor como Visual Studio Code o cualquier otro de su gusto. Escriba el siguiente código y guardelo con el 
  nombre ``test.py``

  .. code-block:: python

     print('Hola desde UPB! conteo hasta 10:')
     for i in range(1,11):
         print(i)

* Ejecute la siguiente línea en la terminal de comandos. Cambio serial_port por el puerto correspondiente en su computador::

    ampy --port serial_port run test.py

  Si al ejecutar el programa ocurre un error, puede ser que tenga abierto el REPL y por tanto deberá cerrarlo ya que 
  ampy intentará abrir el puerto serial al cual está conectado el ESP8266. ¿Cuál es el resultado? tenga en cuenta que si 
  el programa requiere una entrada, será necesario ejecutarlo desde la interfaz REPL.

* Por defecto el comando run esperará a que el programa termine antes de imprimir el resultado; sin embargo, algunos 
  programas se quedarán en un ciclo infinito y nunca retornarán. En estos casos se debe adicionar la opción ``--no-output``. 
  De esta manera ampy no esperará la terminación del programa. Para probar lo anterior, modifique el programa así:

  .. code-block:: python

     import time

     print('Hola desde UPB! contando:')
     while True:
        print(i)
        i += 1
        time.sleep(1)

* Ejecute el programa así::

    ampy --port serial_port run  --no-output test.py

* Luego abra la interfaz REPL para observar el resultado.

* Cuando se escriben programas utilizando el framework de arduino, se emplean dos funciones: ``setup()`` y ``loop()``. 
  La función setup() se ejecuta sólo una vez mientras que la función loop() se repite indefinidamente. Esta estructura 
  de código se puede recrear un micropython:
  
   .. code-block:: python

        ##################
        # código setup
        ##################
        import time

        print('Hola desde UPB! contando:')
        i = 1
        while True:
        ##################
        # código loop
        ##################
            print(i)
            i += 1
            time.sleep(1)

* ampy también permite manipular el sistema de archivos de micropython. Es posible copiar archivos en el ESP8266, leerlos y 
  crear directorios. Copie el archivo test.py en la tarjeta::

    ampy --port /serial/port put test.py

  Para verificar el resultado ejecute:

    ampy --port /serial/port ls

* Para leer archivos::

    ampy --port /serial/port get boot.py

* También es posible compiar el contenido de boot.py en el computador especificando un nombre de archivo::

    ampy --port /serial/port get boot.py board_boot.py

* Para borrar un archivo::

    ampy --port /serial/port rm test.py

* Para borrar un directorio con todo su contenido::

    ampy --port /serial/port rmdir nombre_directorio

* En micropython existen dos archivos importantes: boot.py y main.py. Actualmente main.py no lo hemos creado. ``booy.py`` 
  será ejecutado automáticamente cuando la tarjeta se encienda o se presione el botón reset (RST). Si el archivo 
  ``main.py`` existe, micropython lo ejecutará luego de boot.py. Por tanto, en ``main.py`` debemos escribir el código 
  que deseamos que se ejeucte cada que la tarjeta se encienda. Tenga en cuenta que este programa quedará almacenado y la 
  tarjeta se comportará como lo especifiquemos allí. Para probar lo anterior, ejecute::

    ampy --port /serial/port put test.py /main.py

  Esto hará que el código que hemos venido utilizando se almacene en la tarjeta como main.py. Para probarlo, descenecte 
  y conecte de nuevo la tarjeta e ingrese a la inferfaz REPL. ¿Cuál es el resultado?

En resumen, el flujo de trabajo será así:

1. Escribir el programa en el computador utilizando su editor de texto favorito. Estructure el código con una sección 
   setup y otra loop.
2. Utilice ``ampy`` con la opción ``--no-output`` para correr el script en la tarjeta.
3. Edite el programa tantas veces como haga falta hasta que funcione como desea
4. Si desea que el programa corra automáticamente cada que la tarjeta se encienda utilice ``ampy`` con el comando ``puy`` 
   salvando el archivo con el nombre ``main.py``

Ejercicio: retos
-----------------
El propósito de estos ejercicios será practicar lo aprendido hasta ahora:

Reto 1:
^^^^^^^^
Escriba un programa que lea el radio y la altura de un cilindro (debe preguntarle al usuario) y luego imprima 
el área y el volumen.

Reto 2:
^^^^^^^^
Repita de nuevo el programa anterior pero esta vez cree y utilice funciones para calcular el área y el volumen.

Reto 3:
^^^^^^^^
Escriba un programa que lea un palabra (le pregunta al usuario) y luego imprima cada una de las letras que la componen.

Reto 4:
^^^^^^^^
Escriba un programa que permita calcular: suma, resta, multiplicación y división. El programa debe preguntarle al usuario 
la operación y los operandos. Luego de una operación, el programa debe preguntar si se desea continuar, de lo contrario 
se debe terminar.

Ejercicio: capacidades de entrada-salida del ESP8266 y micropython
-------------------------------------------------------------------


# Trabajo Práctico 0

* Vázquez Lareu, Román
* 100815

## Paso 0 - Entorno de trabajo

1. <br> ![Captura con y sin Valgrind](/valgrind.png)
2. *Valgrind* sirve para debuggear, ayudando a detectar problemas en el manejo de memoria y de threading. La opción mas importante es la de seleccionar el tool: uno posible y a su vez el más común que viene por default es la de memcheck, que indica que toda la memoria allocada sea debidamente liberada. Según la documentación, otro toolname popular es cachegrind, que indica todo lo referido a la memoria cache en la ejecución del programa (referencias y misses tanto de datos como de instrucciones). En cuanto a opciones otras posibles son -q (solo imprime errores de mensaje), -v (imprime información adicional), --vgdb=yes (permite debuggear utilizando GDB), entre otras.
3. *sizeof()* devuelve el tamaño de un tipo de dato o expresión en bytes. el *sizeof(char)* devuelve 1 (byte) y el *sizeof(int)* devuelve 4 (bytes), aunque en el caso del int podría variar dependiendo de la arquitectura y del compilador.
4. el *sizeof()* de un struct puede no ser igual a la suma de los *sizeof()* de cada uno de sus elementos. Cuando se hace el *sizeof()* del struct en su totalidad, se tiene en cuenta el padding, por lo que si el struct tiene un elemento char y uno int el *sizeof()* del struct será 8 (4 del int, 1 del char y 3 del padding del char). Ahora bien, al hacer la suma por separada el valor será 5 (4 del int y 1 del char) ya que no se tiene en cuenta el padding. En el caso de que el struct se encuentre formado únicamente por elementos de tipo int, no se daría esta diferencia.
5.


## Paso 1 - Errores de generación y normas de programación

1. <br> ![Captura errores estilo paso1](/errorEstiloPaso1.png)


Deberia haber un espacio entre el *while* y el paréntesis que abre la expresión a evaluar.
|Incorrecto | Correcto|
|------------ | -------------|
|<pre lang="C"> while(state != STATE_FINISHED); </pre>|<pre lang="C"> while (state != STATE_FINISHED);</pre>|

El espaciado dentro de los paréntesis debería ser consistente a izquierda y a derecha. Además deberia haber a lo sumo un espacio a cada lado. En este caso hay dos a iquierda y ninguno a derecha. Los operadores siempre van rodeados de espacios. 
|Incorrecto | Correcto|
|------------ | -------------|
|<pre lang="C"> if (  c == EOF) { </pre> | <pre lang="C"> if (c == EOF) { </pre>|

El *else* debería haber estado en la misma linea que el } que cierra el bloque previo. Además, si tiene una llave a derecha o izquierda debería estar la correspondiente del lado opuesto.
|Incorrecto | Correcto|
|------------ | -------------|
|<pre lang="C"> else if (state == STATE_IN_WORD) { </pre>| <pre lang="C"> } else if (state == STATE_IN_WORD) { </pre> |

Debería haber un espacio previo al ( del *if*
|Incorrecto | Correcto|
|------------ | -------------|
|<pre lang="C"> if(strchr(delim_words, c) != NULL) { </pre> | <pre lang="C"> if (strchr(delim_words, c) != NULL) { </pre>|

Los punto y coma no deberían llevar un espacio antes de su utilización
|Incorrecto | Correcto|
|------------ | -------------|
|<pre lang="C"> return next_state ; </pre> | <pre lang="C"> return next_state; </pre>|

Usar *snprintf* en vez de *strcpy*
|Incorrecto | Correcto|
|------------ | -------------|
|<pre lang="C"> strcpy(filepath, argv[1]); </pre> | <pre lang="C"> snprintf(filepath, argv[1]); </pre>|

El *else* debería haber estado en la misma linea que el } que cierra el bloque previo. Además, si tiene una llave a derecha o izquierda debería estar la correspondiente del lado opuesto.
|Incorrecto | Correcto|
|------------ | -------------|
|<pre lang="C"> else {  </pre>| <pre lang="C"> } else { </pre> |

Las lineas deberian tener como máximo 80 caracteres

2. <br> ![Captura errores generación paso1](/errorGeneracionPaso1.png) <br> Al poner el flag -c se genera codigo objeto sin linkear (precompilación + compilación). De esta manera ya sabemos que son errores de compilación y no de linkeo. Lo que ocure es que el compilador no tiene la información suficiente acerca de los tipos y nombres de funciones que aparecen en el código, de ahi que indicia *unkown type* y definición implicita. Incluso podrían ser errores de tipeo. Esto podría solucionarse indicandole al compilador que existe ese tipo y esas funciones, declarandolas al principio del archivo por ejemplo. Incluso no haria falta indicar que hacen las funciones, con solo asegurarle al compilador que existen alcanzaria. También hay que tener en cuenta que los errores viene luego de una linea en la que se indica que se generaba codigo objeto a partir de un .c, esta etapa corresponde al compilador, el linker justamente *linkea* los .o
3. El sistema no reportó ningún *Warning* ya que el flag -Werror indica que todos los warnings son tratados como errores.


## Paso 2 - Errores de generación 2

1. En el *main.c* se agregó `#include "paso2_wordscounter.h"` con las declaraciones de tipos y funciones, se reemplazó `strcpy(filepath, argv[1]);` por  ` memcpy(filepath, argv[1], strlen(argv[1]) + 1);` y se colocó el *else* en la misma linea que el } previo. <br> En el *paso2_wordscounter.c* se modificó de tal manera que pase las normas de codificación pero se invirtió el orden de los include, donde ahora primero se incluye el *paso2_wordscounter.h* y luego las librerías necesarias. <br> El *paso2_wordscounter.h* no tuvo modificaciones.

2. <br> ![verificacion de normas de programacion](/normasProgramacionPaso2.png)
3. <br> ![Error generación de código](/errorGeneracionPaso2.png) <br> El compilador lee los *#include* de arriba hacia abajo, por lo que al poner primero el .h y luego las librerías que precisa, arrojará los errores de tipo desconocido, tanto para *size_t* como para *FILE*. <br> Los errores en *words_counter_getwords* vienen de ... <br> Finalmente, el compilador no reconoce a la función *malloc* ya que ni se encuentra definida por el programador como una funcion propia, ni se incluyó la librería *stdlib.h* que es quien la contiene.

## Paso 3 - Errores de generación 3
1. En el *paso3_wordscounter.c* se agregó un *include* con *stdlib.h* y en *paso3_wordscounter.c* se agregaron *includes* para *string.h* y *stdio.h*
2. <br> ![Error generación de codigo](/errorGeneracionPaso3.png) El mensaje de error se da al momento del *linkear* *paso3_wordscounter.o* y *paso3_main.o*. Esto se da porque la función *wordscounter_destroy* es invocada en *paso3_main.c*, declarada en *paso3_wordscounter.h* pero no implementada en *paso3_wordscounter.c*
## Paso 4
1. Se agregó la implementación de *wordscounter_destroy* en *paso3_wordscounter.c*
2. ![Tda](/resultadoTdaValgrindPaso4.png)
3. ![Long Filename](/resultadoLongFileNameValgrindPaso4.png)
4. strncpy
5. buffer overflow y segmentation fault
## Paso 5
## Paso 6
## Paso 7 
## Paso 8

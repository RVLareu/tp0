# Trabajo Práctico 0

* Vázquez Lareu, Román
* 100815

## Paso 0

1. <br> ![Captura con y sin Valgrind](/valgrind.png)
2. *Valgrind* sirve para debuggear, ayudando a detectar problemas en el manejo de memoria y de threading. La opción mas importante es la de seleccionar el tool: uno posible y a su vez el más común que viene por default es la de memcheck, que indica que toda la memoria allocada sea debidamente liberada. Según la documentación, otro toolname popular es cachegrind, que indica todo lo referido a la memoria cache en la ejecución del programa (referencias y misses tanto de datos como de instrucciones). En cuanto a opciones otras posibles son -q (solo imprime errores de mensaje), -v (imprime información adicional), --vgdb=yes (permite debuggear utilizando GDB), entre otras.
3. *sizeof()* devuelve el tamaño de un tipo de dato o expresión en bytes. el *sizeof(char)* devuelve 1 (byte) y el *sizeof(int)* devuelve 4 (bytes), aunque en el caso del int podría variar dependiendo de la arquitectura y del compilador.
4. el *sizeof()* de un struct puede no ser igual a la suma de los *sizeof()* de cada uno de sus elementos. Cuando se hace el *sizeof()* del struct en su totalidad, se tiene en cuenta el padding, por lo que si el struct tiene un elemento char y uno int el *sizeof()* del struct será 8 (4 del int, 1 del char y 3 del padding del char). Ahora bien, al hacer la suma por separada el valor será 5 (4 del int y 1 del char) ya que no se tiene en cuenta el padding. En el caso de que el struct se encuentre formado únicamente por elementos de tipo int, no se daría esta diferencia.
5.


## Paso 1

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

Debería haber un espacio previo al ( del if
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

2. <br> ![Captura errores generación paso1](/errorGeneracionPaso1.png)
3. El sistema no reportó ningún *Warning* ya que el flag -Werror indica que todos los warnings son tratados como errores.


## Paso 2

1. En el *main.c* se agregó `#include "paso2_wordscounter.h"`, se reemplazó `strcpy(filepath, argv[1]);` por  ` memcpy(filepath, argv[1], strlen(argv[1]) + 1);` y se colocó el *else* en la misma linea que el } previo

2. <br> ![verificacion de normas de programacion](/normasProgramacionPaso2.png)
3. <br> ![Error generación de código](/errorGeneracionPaso2.png)

# Trabajo Práctico 0

* Vázquez Lareu, Román
* 100815

## Paso 0

1. ![Captura con y sin Valgrind](/valgrind.png)
2. *Valgrind* sirve para debuggear, ayudando a detectar problemas en el manejo de memoria y de threading. La opción mas importante es la de seleccionar el tool: uno posible y a su vez el más común que viene por default es la de memcheck, que indica que toda la memoria allocada sea debidamente liberada. Según la documentación, otro toolname popular es cachegrind, que indica todo lo referido a la memoria cache en la ejecución del programa (referencias y misses tanto de datos como de instrucciones). En cuanto a opciones otras posibles son -q (solo imprime errores de mensaje), -v (imprime información adicional), --vgdb=yes (permite debuggear utilizando GDB), entre otras.
3. *sizeof()* devuelve el tamaño de un tipo de dato o expresión en bytes. el *sizeof(char)* devuelve 1 (byte) y el *sizeof(int)* devuelve 4 (bytes), aunque en el caso del int podría variar dependiendo de la arquitectura y del compilador.
4. el *sizeof()* de un struct puede no ser igual a la suma de los *sizeof()* de cada uno de sus elementos. Cuando se hace el *sizeof()* del struct en su totalidad, se tiene en cuenta el padding, por lo que si el struct tiene un elemento char y uno int el *sizeof()* del struct será 8 (4 del int, 1 del char y 3 del padding del char). Ahora bien, al hacer la suma por separada el valor será 5 (4 del int y 1 del char) ya que no se tiene en cuenta el padding. En el caso de que el struct se encuentre formado únicamente por elementos de tipo int, no se daría esta diferencia.
5.

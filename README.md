# Simulador de selector de aliens basado en el omnitrix de la serie "Ben 10"
Como dice el título, este proyecto se basa en el misterioso comportamiento interno que tiene el Omnitrix en la serie Ben 10,
donde para usarse se sigue el siguiente comporamiento:

>Ejemplo 1: Augmentine "125" suspensión, (125/31,25 mg/5 ml)
> 
>Paso 1: Introducir el peso del paciente. Por ejemplo: 8 kg.
>Paso 2: Introducir la posología deseada. Por ejemplo: 40 mg/kg/día.
>Paso 3: Introducir la presentación. Suspensión.
> 
>Con estos datos se obtiene la dosis al día: 320 mg/día.
>
>Paso 4: Elegir el número de dosis al día: 3 dosis = cada 8 horas.
>Paso 5: Introducir los mg que contiene la unidad (en este caso el ml).
>            Si la concentración es de 125 mg/5 ml. Los mg/ml = 125/5 = 25 mg/ml.
>            Para resolver este cálculo tenemos a la derecha otra calculadora.
>
>Obtenemos: 106,67 mg/dosis = 4,28 ml cada 8 horas.

Adicionalmente incluyo las funciones para registrar nuevo medicamentos y ver los medicamentos registrados 
por orden alfabético o por cantidad  de gramaje 

## SICT0302B: Toma decisiones 

### Selecciona y usa una estructura lineal adecuada al problema

Uso un queue en la parte del modo de selección guiada para sacar los aliens en un orden descendente y no repetirlos, y para almacenar los aliens un simple vector.
Cada alien es un objeto que contiene como atributos de tipo entero: inteligencia, fuerza, velocidad, resistencia, total, batallas ganadas, veces usado y veces elegido;
y el nombre que es un atributo de tipo cadena. Los cinco primeros atributos se usan para poder ordenar a los aliens según el criterio deseado en el modo de selección
guiada, a su vez, total, batallas ganadas y veces elegido se usan para el orden en el splay tree.


### Selecciona un algoritmo de ordenamiento adecuado al problema

Para este problema utilice dos algoritmos de ordenamiento distintos, uno de tipo InsertionSort y otro de tipo MergeSort, específicamente si hay 20 aliens o menos se usará el 
Insertion Sort y si hay más (en la serie original la versión del futuro de Ben 10 llegó a tener más de 10,000 aliens) se usará el MergeSort. La razón de esto es que cuando hay
un número pequeño de elementos InsertionSort puede ser igual o incluso más eficiente que MergeSort en algunos casos, y MergeSort porque de los que vimos en clase es el más 
eficiente ya que su complejidad temporal no depende de cómo estén ordenados los elementos.
Las fuciones donde se pueden ver es en las funciones insertionSort (línea 26) y mergeSort (línea 151) en el archivo ordenamiento.h, he de mencionar también que mergeSort
requiere de otras funciones para funcionar como mergeArray (línea 73) y mergeSplit (línea 125).

### Usa un árbol adecuado para resolver un problema

Usé un Splay Tree para poder acceder rapidamente a los aliens usados recientemente y que estén acomodados en base a 3 criterios (veces seleccionado,
batallas ganadas y por último total), la lógica es que si dos aliens tienen el mismo número de veces seleccionado se usará batallas ganadas y si este
otro atributo también es igual se usará total (atributo que es la suma de otros 4, lo cual dificulta que se repita). 

Las funciones donde lo uso es en seleccionLibre de menu.h en la linea 437 (utiliza registrarEleccionSplay en la línea 32 de omnitrix.h que a su vez ocupa find de la clase SplayTree
y find de la clase Node, líneas 591 y 112 respecitvamente de arbol.h ), registrarAlien en la línea 187 de menu.h (utiliza anadirAlien de omnitrix.h línea 86 y anadirSplay en línea 26, 
esta última utiliza add de las clases Node y SplayTree, ambas declaradas en arbol.h línea 67 y 542 respectivamente ).
Finalmente eliminarADN de menu.h línea 295 (utiliza eliminarAlienSplay declarada en la línea 29 de omnitrix.h que a su vez usa remove de las clases Node y SplayTree, y se declaran
en arbol.h líneas 189 y 554 respectivamente). 

## SICT0301B: Evalúa los componentes

### Presenta Casos de Prueba correctos y completos para todas las funciones y procedimientos del programa,

Honestamente, aún no he implementado casos de prueba, pero los que planeo son los siguientes:

Añadir y eliminar aliens.

Probar los distintos ordenamientos haciendo ordenamiento con los 20 por defecto y luego con otro que añada yo.

Y las distintas funciones que involucran al SplayTree, pudiendo verificar que todo esté en orden con la función printTree.

El guardado también sería importante de verificar, sobre todo en el splay tree.

### Hace un análisis de complejidad correcto y completo para todo el programa y sus compenetes,

#### Vector y Splay Tree de aliens

función de selección guiada: 

funcion de selección libre: 

función de añadir alien: 

#### ordenamiento de medicinas

ordenamiento con merge sort: ...

#### uso de árbol

crear árbol de gramaje: ...

agregar nodo a árbol gramaje: ...

econtrar nodo en árbol gramaje: ...

## SICT0303B: Implementa acciones científicas 

### Implementa mecanismos para consultar información de las estructuras correctos y útiles dentro de un programa.

El programa tiene la opción de buscar medicinas en base a 5 criterios distintos, o en base al nombre.
El programa permite obtener información acerca de todos los aliens o el que se especifique.

### Implementa mecanismos de lectura de archivos correctos y útiles dentro de un programa. Usar de manera

Los aliens así como su información, se encuentran almacenados en un archivo llamado "prueba.txt", tanto las características como las conexiones en el splay tree.

### Implementa mecanismos de escritura de archivos correctos y útiles dentro de un programa. Usar de manera

Los aliens se guardan al final de cada ejecución del programa para no tener que registrarlos todos cada vez que se vayan a usar.

# Simulador de selector de aliens basado en el omnitrix de la serie "Ben 10"
Como dice el título, este proyecto se basa en el misterioso comportamiento interno que tiene el Omnitrix en la serie Ben 10,
donde para usarse se sigue el siguiente comportamiento:

>Ejemplo 1: Selección guiada 
> 
>Paso 1: Introducir el criterio de selección, puede ser fuerza, velocidad, resistencia, una combinación de estos o el total,
>en caso de no ser válido se usará velocidad o resistencia por defecto (según sea modo de un criterio o dos).
>Paso 2: Ver los aliens que van saliendo hasta que se desee.
>Ejemplo 2: Selección libre 
>
>Paso 1: Insertar el nombre del alien que quieres elegir (tienes intentos limitados que se reinician cuando eliges un alien no repetido y válido)
>Paso 2: Continuar eligiendo aliens (no puedes elegir el mismo dos veces seguidas) hasta que se desee o se agote el número de intentos.
>            

Adicionalmente incluyo funciones para registrar nuevos aliens, eliminarlos, ver un alien en base al nombre y sus estadísticas, ver la lista de aliens completa o ver la lista con atributos incluso. 
El orden de los aliens en las "listas" es en el que se hayan añadido, nunca modifico dicho vector para que así se sepa siempre en qué orden se añadieron.

## SICT0302B: Toma decisiones 

### Selecciona y usa una estructura lineal adecuada al problema

Uso un queue en la parte del modo de selección guiada ya que están ordenados para sacar los aliens en un orden descendente y no repetirlos; para almacenar los aliens uso un simple vector.
Cada alien es un objeto que contiene como atributos de tipo entero: inteligencia, fuerza, velocidad, resistencia, total, batallas ganadas, veces usado y veces elegido;
y el nombre que es un atributo de tipo cadena. Los cinco primeros atributos se usan para poder ordenar a los aliens según el criterio deseado en el modo de selección
guiada; a su vez: total, batallas ganadas y veces elegido se usan para determinar el orden en el splay tree.


### Selecciona un algoritmo de ordenamiento adecuado al problema

Para este problema utilice dos algoritmos de ordenamiento distintos, uno de tipo InsertionSort y otro de tipo MergeSort, específicamente si hay 20 aliens o menos se usará el 
Insertion Sort y si hay más (en la serie original la versión del futuro de Ben 10 llegó a tener más de 10,000 aliens) se usará el MergeSort. La razón de esto es que, cuando hay
un número pequeño de elementos, InsertionSort puede ser igual o incluso más eficiente que MergeSort en algunos casos, y elegí MergeSort porque de los que vimos en clase es el más 
eficiente ya que su complejidad temporal no depende de cómo estén ordenados los elementos (lo cual es bueno para el peor caso pero afecta un poco al mejor).
InsertionSort (línea 26) y mergeSort (línea 151) están en el archivo ordenamiento.h, he de mencionar también que mergeSort requiere de otras funciones para funcionar como mergeArray 
(línea 73) y mergeSplit (línea 125).

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

Añadir y eliminar aliens y posteriormente mostrar la lista de aliens para ver si están todos los añadidos y si están en el orden que se fueron insertando.

Probar los distintos ordenamientos haciendo ordenamiento con los 20 por defecto y luego con otro que añada yo.

Añadir alien, selección libre y eliminar ADN peligroso involucran al SplayTree, se puede hacer dichas operaciones y luego pedir la lista de aliens o usar el printTree.

El guardado se puede probar haciendo modificaciones al añadir aliens y/o eliminarlos, cerrar el programa y luego volver a abrirlo y pedir ver la lista de aliens.

### Hace un análisis de complejidad correcto y completo para todo el programa y sus componentes,

#### Vector y Splay Tree de aliens

función de selección guiada: 

funcion de selección libre: 

función de añadir alien: 

#### ordenamiento de aliens

selección guiada en base a un parámetro / balanceada: ...

selección guiada en base a dos parámetros:

#### uso de árbol

crear árbol de aliens: ...

agregar alien (nodo) a árbol: ...

econtrar alien (nodo) en árbol : ...

eliminar alien (nodo) en árbol: ...

## SICT0303B: Implementa acciones científicas 

### Implementa mecanismos para consultar información de las estructuras correctos y útiles dentro de un programa.

El programa tiene la opción de mostrar aliens en base a 5 criterios compuestos o a la elección de 2 de los 4, o en base al nombre.
El programa permite obtener información acerca de todos los aliens o el que se especifique.

### Implementa mecanismos de lectura de archivos correctos y útiles dentro de un programa. Usar de manera

Los aliens así como su información, se encuentran almacenados en un archivo llamado "prueba.txt", también los nodos y sus conexiones.
### Implementa mecanismos de escritura de archivos correctos y útiles dentro de un programa. Usar de manera

Los aliens se guardan al final de cada ejecución del programa para no tener que registrarlos todos cada vez que se vayan a usar.

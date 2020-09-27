# [Arreglos](#arrays)

Contenedores de un número fijo de datos del mismo tipo.
El tamaño se define cuando se crean.
Cada elemento del arreglo se le conoce como `elemento` y puede ser accedido a través de un `índice` numérico.

```java
int[] anArray;
anArray = new int[10];
anArray[0] = 100;
anArray[1] = 200;
anArray[2] = 300;
anArray[3] = 400;
anArray[4] = 500;
anArray[5] = 600;
anArray[6] = 700;
anArray[7] = 800;
anArray[8] = 900;
anArray[9] = 1000;

System.out.println(anArray[4]); // 500
```

## [Declaración de variable que referencia a un arreglo](#declaring-variable-to-refer-to-an-array)

La declaración de un arreglo posee dos componentes: el tipo del arreglo: `type []`, donde `type` es el tipo de datos que contendrá el arreglo, y el nombre de la variable. Esto indicará que se ha creado una variable que contendrá un arreglo, sin embargo el valor de dicha variable y el tamaño del arreglo aun no se definen.

```java
byte[] anArrayOfBytes;
short[] anArrayOfShorts;
long[] anArrayOfLongs;
float[] anArrayOfFloats;
double[] anArrayOfDoubles;
boolean[] anArrayOfBooleans;
char[] anArrayOfChars;
String[] anArrayOfStrings;
```

## [Creando, inicializando y accediendo a arreglo](#creating-initializing-accesing-array)

Para crear un arreglo se usa el operador `new`. 

```java
int[] anArray = new int[10];
```

Para asignar valores usamos los `índices`:

```java
anArray[0] = 100;
anArray[1] = 200;
anArray[2] = 300;
```

Para acceder a los valores también usamos los `índices`:

```java
System.out.println("Element 1 at index 0: " + anArray[0]);
System.out.println("Element 2 at index 1: " + anArray[1]);
System.out.println("Element 3 at index 2: " + anArray[2]);
```

También es posible usar la lista inicializadora para inicializar un arreglo:

```java
int[] anArray = { 
    100, 200, 300,
    400, 500, 600, 
    700, 800, 900, 1000
};
```

También pueden crearse arreglos de arreglos (matrices):

```java
String[][] names = {
    {"Mr. ", "Mrs. ", "Ms. "},
    {"Smith", "Jones"}
};

// Mr. Smith
System.out.println(names[0][0] + names[1][0]);
// Ms. Jones
System.out.println(names[0][2] + names[1][1]);
```

Para conocer el tamaño de un arreglo podemos usar `length`:

```java
System.out.println(anArray.length);
```

## [Copiando arreglos](#copying-arrays)

Es posible copiar un arreglo usando `System.arraycopy(...)`. Aqui se muestra el prototipo del método:

```java
public static void arraycopy(Object src, int srcPos,
                             Object dest, int destPos, int length)
```

Por ejemplo:

```java
char[] copyFrom = { 'd', 'e', 'c', 'a', 'f', 'f', 'e',
                    'i', 'n', 'a', 't', 'e', 'd' };
char[] copyTo = new char[7];

System.arraycopy(copyFrom, 2, copyTo, 0, 7);
System.out.println(new String(copyTo)); // caffein
```

## [Manipulación de arreglos](#arrays-manipulation)

Para la mayor cantidad de operaciones con arreglos utilice la clase `java.util.Arrays`. Existen operaciones como:

- Buscar en el arreglo un valor específico para obtener el índice (`binarySearch`).
- Comparar arreglos (`equals`).
- Llenar un arreglo hasta un determinado índice (`fill`).
- Ordenar un arreglo en forma ascendente. Puede usar `sort`, y si quiere un ordenamiento paralelo use `parallelSort`.
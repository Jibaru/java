# [Sentencias de control de flujo](#control-flow-statements)


## [Sentencia if-then](#if-then-statement)

Le dice al programa que se va a ejecutar una sección del código únicamente si se evalúa la condición como verdadera.

```java
// the "if" clause: bicycle must be moving
if (isMoving){ 
    // the "then" clause: decrease current speed
    currentSpeed--;
}
```

Es posible remover los `{}` si la sentencia `if` solo contiene una expresión.

```java
if (isMoving)
    currentSpeed--;
```

## [Sentencia if-then-else](#if-then-else-statement)

Provee a la sentencia `if` una segunda parte, que se ejecutará únicamente si la evaluación anteriormente mencionanda devuelve `false`.

```java
if (isMoving) {
    currentSpeed--;
} else {
    System.err.println("The bicycle has already stopped!");
}
```

## [Sentencia switch](#switch-statement)

Provee mayor posibilidades al momento de evaluar una expresión. La expresión puede evaluarse si son: `byte`, `short`, `char`, `int`. También funciona con `tipos enumerados`, la clase `String`, `Character`, `Byte`, `Short` e `Integer`.

```java
int month = 8;
String monthString;
switch (month) {
    case 1:  monthString = "January";
                break;
    case 2:  monthString = "February";
                break;
    case 3:  monthString = "March";
                break;
    case 4:  monthString = "April";
                break;
    case 5:  monthString = "May";
                break;
    case 6:  monthString = "June";
                break;
    case 7:  monthString = "July";
                break;
    case 8:  monthString = "August";
                break;
    case 9:  monthString = "September";
                break;
    case 10: monthString = "October";
                break;
    case 11: monthString = "November";
                break;
    case 12: monthString = "December";
                break;
    default: monthString = "Invalid month";
                break;
}
System.out.println(monthString); // August
```

El cuerpo del `switch` es llamada `bloque switch` y puede tener uno o más `case` o algún `default`. La palabra `break` evita que se sigan ejecutando los demás `case` en caso llegue a hacer match con el valor evaluado.

<b>Nota: </b> si se evalúan instancias de las clase `String` hay que cerciorarse de que éstas no sean `null` porque produciría un `NullPointerException` al ser evaluadas con el método `String.equals`.

## [Sentencia while y do-while](#while-and-do-while-statements)

La sentencia `while` ejecuta un bloque de sentencias si la condición evaluada es `true`.

```java
while (expression) {
    statement(s)
}
```

La sentencia `do-while` ejecuta primero el bloque `do` para después evaluar la condición.

```java
do {
    statement(s)
} while (expression);
```

## [La sentencia for](#for-statement)

Provee una forma compacta de iterar sobre un rango de valores.

```java
for (inicializacion; condición; incremento) {
    statement(s)
}
```

- La sección de `inicialización` se ejecuta al inicio una única vez.
- La `condición` será evaluada por cada iteración. En caso de ser `false`, terminará el loop.
- El `incremento` se ejecutará después de cada iteración. Normalmente suele ir una expresión que incremente o decremente un valor.

Las tres expresiones mencionadas son opcionales.

```java
for(int i = 1; i < 11; i++){
    System.out.println("Count is: " + i);
}
```

Para recorrer `arreglos` o `Colecciones` es preferible usar el `for mejorado`.

```java
int[] numbers = {1,2,3,4,5,6,7,8,9,10};
for (int item : numbers) {
    System.out.println("Count is: " + item);
}
```

En el ejemplo, `item` recibirá los valores del arreglo `numbers` por cada iteración. El loop terminará cuando no existan más elementos en el arreglo por recorrer.

## [Sentencias de bifurcación](#branching-statements)

### [Sentencia break](#break-statement)

La sentencia break tiene dos formas: etiquetada y no etiquetada.

Para terminar un ciclo `for`, `while` o `do-while` puede usar el `break` etiquetado.

```java
int[] arrayOfInts = { 32, 87, 3, 589, 12, 
                    1076, 2000, 8, 622, 
                    127 };
int searchfor = 12;

int i;
boolean foundIt = false;

for (i = 0; i < arrayOfInts.length; i++) {
    if (arrayOfInts[i] == searchfor) {
        foundIt = true;
        break;
    }
}
```

El `break etiquetado` puede terminar una sentencia externa.

```java
int[][] arrayOfInts = { 
            { 32, 87, 3, 589 },
            { 12, 1076, 2000, 8 },
            { 622, 127, 77, 955 }
};
int searchfor = 12;

int i;
int j = 0;
boolean foundIt = false;

search:
    for (i = 0; i < arrayOfInts.length; i++) {
        for (j = 0; j < arrayOfInts[i].length;
                j++) {
            if (arrayOfInts[i][j] == searchfor) {
                foundIt = true;
                break search;
            }
        }
    }

System.out.println("Found " + searchfor + 
" at " + i + ", " + j); // Found 12 at 1, 0
```

### [Sentencia continue](#continue-statement)

Salta una iteración en un `for`, `while` o `do-while` 

El `continue no equiquetado` salta al final del loop y evalúa la condición que controla al loop. 

```java
String searchMe = "peter piper picked a " +
 "peck of pickled peppers";
int max = searchMe.length();
int numPs = 0;

for (int i = 0; i < max; i++) {
    // interested only in p's
    if (searchMe.charAt(i) != 'p')
        continue;

    // process p's
    numPs++;
}
System.out.println("Found " + numPs + 
" p's in the string."); // Found 9 p's in the string.
```

El `continue etiquetado` salta la iteración con la etiqueta correspondiente.

```java
String searchMe = "Look for a substring in me";
    String substring = "sub";
    boolean foundIt = false;

    int max = searchMe.length() - 
                substring.length();

test:
    for (int i = 0; i <= max; i++) {
        int n = substring.length();
        int j = i;
        int k = 0;
        while (n-- != 0) {
            if (searchMe.charAt(j++) != substring.charAt(k++)) {
                continue test;
            }
        }
        foundIt = true;
            break test;
    }
System.out.println(foundIt ? 
"Found it" : "Didn't find it"); // Found it
```

### [Sentencia return](#return-statement)

Sale del método actual y el control de flujo se devuelve al lugar donde se llamó al método.

Puede devolver un valor:

```java
return ++count;
```

O simplemente puede no retorna nada (cuando un método es declarado `void`).

```java
return;
```
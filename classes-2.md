# [Más sobre las clases](#more-on-classes)

## [Retornando un valor desde un método](#returning-a-value-from-a-method)

Un método vuelve al lugar donde fue llamado cuando:

- Completa todas las sentencias dentro de él.
- Devuelve un valor con `return` o
- tira una excepción.

Para devolver un valor cuando el método no sea `void` use:

```java
return returnValue;
```

Donde el tipo de `returnValue` tiene que ser igual al tipo de retorno del método.

Es posible devolver valores con tipos primitivos:

```java
public int getArea() {
    return width * height;
}
```

Y también valores con tipos de referencia:

```java
public Bicycle seeWhosFastest(Bicycle myBike, 
Bicycle yourBike, Environment env) {
    Bicycle fastest;
    // code to calculate which bike is 
    // faster, given each bike's gear 
    // and cadence and given the 
    // environment (terrain and wind)
    return fastest;
}
```

### [Devolviendo una clase o interface](#returning-a-class-or-interface)

Es posible retornar tipos que sean una clase o subclase.

Suponiendo que hubiese una clase `Numbers` y otra clase `ImaginaryNumbers` que hereda de la primera, podría escribir un método que devuelva el tipo de la superclase:

```java
public Number returnANumber() {
    ...
}
```

Es decir, el método podría devolver objetos de tipo `Number` o `ImaginaryNumber`.

Si solo devolviera objetos de la clase hija, podría sobreescribir el método:

```java
public ImaginaryNumber returnANumber() {
    ...
}
```

A esta técnica se la conoce como `tipo de retorno covariante`, significa que el tipo de retorno puede variar en la misma dirección que la subclase.

Lo mismo puede aplicarse para interfaces y clases que implementen dichas interfaces.

## [Palabra reservada this](#keyword-this)

Dentro de un constructor o método, `this` hace referencia al objeto actual.

### [Usando this con un campo](#using-this-with-a-field)

Para acceder a algun campo use `this.field`. Es probable que en constructores o métodos quiera usar dicha notación:

```java
public class Point {
    public int x = 0;
    public int y = 0;
        
    //constructor
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

### [Usando this con un constructor](#using-this-with-a-constructor)

Es posible invocar a un constructor de la misma clase dentro de otro constructor usando `this.(...)`

```java
public class Rectangle {
    private int x, y;
    private int width, height;
        
    public Rectangle() {
        this(0, 0, 1, 1);
    }
    public Rectangle(int width, int height) {
        this(0, 0, width, height);
    }
    public Rectangle(int x, int y, int width, int height) {
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
    }
    ...
}
```

## [Controlando el acceso a miembros de la clase](#controlling-access-to-members-of-a-class)

Los modificadores de acceso determinan que clases pueden acceder a los miembros o métodos de otra clase.

Se pueden aplicar a una clase o a un miembro o método de la clase.

La siguiente tabla muestra todos los modificadores y quienes tienen acceso:

| Modificador | Clase | Paquete | Subclase | Todos |
|-------------|:-----:|:-------:|:--------:|:-----:|
|public       | Si    | Si      | Si       | Si    |
|protected    | Si    | Si      | Si       | No    |
|sin modifi.  | Si    | Si      | No       | No    |
|private      | Si    | No      | No       | No    |

## [Entendiendo los miembros de clase](#understanding-class-members)

### [Variables de clase](#class-variables)

Cuando varias instancias poseen un miembro que va a ser común a todas en cuanto a valor se recomienda usar un miembro de clase usando el modificador `static`. Cuando una variable se declara como `static` es compartida entre todas las instancias.

```java
public class Bicycle {
        
    private int cadence;
    private int gear;
    private int speed;
        
    // add an instance variable for the object ID
    private int id;
    
    // add a class variable for the
    // number of Bicycle objects instantiated
    private static int numberOfBicycles = 0;

    public Bicycle(int startCadence, int startSpeed, int startGear){
        gear = startGear;
        cadence = startCadence;
        speed = startSpeed;

        // increment number of Bicycles
        // and assign ID number
        id = ++numberOfBicycles;
    }
    
}
```

Las variables de clase pueden ser referenciadas a traves del nombre de la clase:

```java
Bicycle.numberOfBicycles
```

### [Métodos de clase](#class-methods)

De la misma forma que las variables de clase, al agregar el modificador `static` a un método este se convierte a un método de clase que puede ser compartido por cualquier instancia.

```java
public static int getNumberOfBicycles() {
    return numberOfBicycles;
}
```

Para acceder a un método de clase use la siguiente sintaxis:

```java
ClassName.methodName(args)
```

Debe tener en cuenta que:

- Los `métodos de instancia` pueden acceder a variables de instancia, métodos de instancia, variables de clase y métodos de clase directamente.
- Los `métodos de clase` pueden acceder a variables de clase y métodos de clase directamente, pero para acceder a variables y métodos de instancia necesitan de una referencia a la instancia. Tampoco poseen acceso a la palabra `this` (puesto que no hay instancia a la cual referirse).

### [Constantes](#constants)

La combinación de `static` con `final` sirven para definir una constante. El modificador `final` indica que el valor no va a cambiar.

```java
static final double PI = 3.141592653589793;
```

Por convención las constantes se escriben en mayúsculas separando palabras por `_`.

Cada vez que cambie el valor de una constante en alguna clase, recompile para que el cambio se vea afectado en algún otro lugar donde se utilice dicha constante.

## [Inicializando campos](#initializing-fields)

Es posible proveer a un campo de un valor inicial asignando un valor en la declaración.

```java
public class BedAndBreakfast {

    // initialize to 10
    public static int capacity = 10;

    // initialize to false
    private boolean full = false;
}
```

Si la inicialización requiere de computar un valor (a traves de métodos o con bucles) se sugiere usar el constructor.

Para las variables de clase (puesto que no pueden inicializarse con el constructor) use los `bloques  de inicialización static`.

### [Bloques de inicialización static](#static-initialization-blocks)

Use la siguiente sintaxis para los bloques de inicialización static:

```java
static {
    // whatever code is needed for initialization goes here
}
```

Es posible tener cero o más bloques de inicialización static en una clase, llamándose siempre en orden (de arriba hacia abajo).

Una alternativa a los bloques de inicialización static son la creación de métodos `static` y `private`.

```java
class Whatever {
    public static varType myVar = initializeClassVariable();
        
    private static varType initializeClassVariable() {

        // initialization code goes here
    }
}
```

La ventaja de éstos métodos es que pueden volver a ser llamados si se necesita reinicializar las variables de clase.

### [Inicializando miembros de instancia](#initializing-instance-members)

Normalmente cuando se desea inicializar un miembro de instancia se suele realizar en el constructor. Existen dos formas de hacerlo:

A traves de bloques de inicialización para instancias:

```java
{
    // whatever code is needed for initialization goes here
}
```
Dicho bloque será copiado por el compilador a todos los constructores de la clase.

A traves de métodos finales:

```java
class Whatever {
    private varType myVar = initializeInstanceVariable();
        
    protected final varType initializeInstanceVariable() {

        // initialization code goes here
    }
}
```

Este último es más útil cuando se requiere que una subclase reutilize el método de inicialización. 

<b>Nota: </b>Los métodos finales no pueden ser sobreescritos por una subclase.
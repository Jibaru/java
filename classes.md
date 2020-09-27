# [Clases](#classes)

## [Declaración de clases](#declaring-classes)

```java
class MyClass {
    // field, constructor, and 
    // method declarations
}
```

Declaración completa:

```java
class MyClass extends MySuperClass implements YourInterface {
    // field, constructor, and
    // method declarations
}
```

En general, la declaración de una clase posee lo siguiente:

- Modificador `public` o `private` u otro.
- El nombre de la clase (letra inicial mayúscula) capitalizado.
- El nombre de la superclase precedido de `extends` solamente si hereda de alguna clase.
- Separados por comas la lista de interfaces que implementa, precedidos por `implements`, solamente si implementa alguna interfaz.
- El cuerpo de la clase entre `{}`.

## [Declaración de variables miembro](#declaring-member-variables)

Es importante denotar que:

- Las variables miembro de una clase son llamados `campos o atributos`.
- Las variables en un métodos o bloque son llamadas `variables locales`.
- Las variables en la declaración de un método son llamados `parámetros`.

La declaración de los campos está compuesta por 3 partes:

- Cero o más modificadores como `public` o `private`.
- El tipo del campo.
- El nombre del campo.

```java
public int cadence;
public int gear;
public int speed;
```

### [Modificadores de acceso](#access-modifiers)

Sirven para controlar el acceso a miembros desde otra clase.

- `public` es para poder acceder desde cualquier clase.
- `private` solo podrá acceder a ese miembro desde dentro de la clase.

<b>Nota: </b>Casi siempre se preferirá hacer los campos `private`. Para que otra clase puede acceder a estos se usarán métodos que devuelvan sus valores.

```java
public class Bicycle {
        
    private int cadence;
    private int gear;
    private int speed;
        
    public Bicycle(int startCadence, int startSpeed, int startGear) {
        gear = startGear;
        cadence = startCadence;
        speed = startSpeed;
    }
        
    public int getCadence() {
        return cadence;
    }
        
    public void setCadence(int newValue) {
        cadence = newValue;
    }
        
    public int getGear() {
        return gear;
    }
        
    public void setGear(int newValue) {
        gear = newValue;
    }
        
    public int getSpeed() {
        return speed;
    }
        
    public void applyBrake(int decrement) {
        speed -= decrement;
    }
        
    public void speedUp(int increment) {
        speed += increment;
    }
}
```

### [Tipos](#types)

Se puede usar cualquier tipo primitivo para los miembros. También se pueden usar tipos de referencia como `String`, `arreglos` u `Objetos`.

## [Definiendo métodos](#defining-methods)

Por lo general, los métodos poseen 6 partes:

- Modificadores de acceso.
- Un tipo de retorno. `void` si no devolverá nada.
- El nombre del método.
- La lista de parámetros en paréntesis, delimitados por comas y precedidos por su tipo. Si no hay parámetros irán solo los paréntesis vacíos.
- La lista de excepciones.
- El cuerpo del método, entre `{}`.

```java
public double calculateAnswer(double wingSpan, int numberOfEngines, double length, double grossTons) {
    //do the calculation here
}
```

<b>La signatura de un método: </b>Son el nombre y los tipos de parámetros del método.

```java
calculateAnswer(double, int, double, double)
```

### [Nombrando un método](#naming-a-method)

Por convención, los métodos inician por verbos en minúscula. Si son una frase, deberán ser adjetivos o sinónimos. La primera letra es en minúscula, el resto es capitalizado.

```java
run
runFast
getBackground
getFinalData
compareTo
setX
isEmpty
```

### [Métodos sobrecargados](#overloading-methods)

Es posible tener métodos con el mismo nombre si su signatura es diferente, es decir:

- La cantidad de parámetros es diferente y/o
- El tipo de parámetros es diferente

```java
public class DataArtist {
    ...
    public void draw(String s) {
        ...
    }
    public void draw(int i) {
        ...
    }
    public void draw(double f) {
        ...
    }
    public void draw(int i, double f) {
        ...
    }
}
```

## [Constructores](#constructors)

Lucen igual a los métodos solo que no poseen un tipo de retorno y poseen el nombre de la clase.

```java
public Bicycle(int startCadence, int startSpeed, int startGear) {
    gear = startGear;
    cadence = startCadence;
    speed = startSpeed;
}
```

Cuando se crea un nuevo objeto se llama al constructor de la clase con el operador `new`:

```java
Bicycle myBike = new Bicycle(30, 0, 8);
```

También es posible sobrecargar constructores, basándose en la lista de argumentos únicamente.

```java
public Bicycle() {
    gear = 1;
    cadence = 10;
    speed = 0;
}
```

Si no se provee de un constructor, el compilador provee un constructor por defecto sin ningún parámetro. Si la clase hereda se otra clase, el constructor por defecto llamará al constructor sin parámetros de la superclase.

De la misma forma los constructores pueden tener modificadores de acceso.

## [Pasando información a un método o constructor](#passing-information-to-a-method-or-a-constructor)

Para pasar información al momento de llamar a un método o constructor estos tienen que estar en el orden de los parámetros y respetar el tipo de éstos. La información que se ingresará a los parámetros son llamados `argumentos`.

### [Tipos de los parámetros](#parameters-type)

Los tipos que pueden usarse como parámetros son los primitivos y de referencia como objetos o arreglos.

<b>Nota: </b> Si se quiere pasar un método como parámetro a otro método use `expresiones lambda` o `referencias a métodos`.

### [Número arbitrario de argumentos](#arbitrary-numbers-of-arguments)

Si no conoce la cantidad de parámetros que puede recibir un método, use `varargs`.

Siempre deberá usarse al final de otros parámetros.

El parámetro podrá usarse como un arreglo en el cuerpo del método.

```java
public Polygon polygonFrom(Point... corners) {
    int numberOfSides = corners.length;
    double squareOfSide1, lengthOfSide1;
    squareOfSide1 = (corners[1].x - corners[0].x)
                     * (corners[1].x - corners[0].x) 
                     + (corners[1].y - corners[0].y)
                     * (corners[1].y - corners[0].y);
    lengthOfSide1 = Math.sqrt(squareOfSide1);

    // more method body code follows that creates and returns a 
    // polygon connecting the Points
}
```

### [Nombre de los parámetros](#parameters-names)

El nombre de los parámetros debe respetar:

- Debe ser único en la lista de parámetros.
- No puede ser igual al nombre de alguna variable local del método o constructor.
- Puede tener el mismo nombre de algún campo de la clase, aunque no es recomendable si no es el constructor o métodos de acceso.

```java
public class Circle {
    private int x, y, radius;
    public void setOrigin(int x, int y) {
        ...
    }
}
```

Para evitar confusiones se recomienda usar `this` para referirse a miembros de clase en caso existan parámetros con el mismo nombre.

### [Pasando argumentos con tipo de datos primitivos](#passing-primitive-data-type-arguments)

Los argumentos con tipos de datos primitivos son pasados por `valor`, es decir si el valor del parámetro es modificado en el método, esto no modificará el valor pasado como argumento.

```java
public class PassPrimitiveByValue {

    public static void main(String[] args) {
           
        int x = 3;
           
        // invoke passMethod() with 
        // x as argument
        passMethod(x);
           
        // print x to see if its 
        // value has changed
        System.out.println("After invoking passMethod, x = " + x);
        // After invoking passMethod, x = 3
    }
        
    // change parameter in passMethod()
    public static void passMethod(int p) {
        p = 10;
    }
}
```

### [Pasando argumentos con tipos de datos de referencia](#passing-reference-data-types-arguments)

Los argumentos con tipos de datos de referencia son pasados por `valor`, <b>sin embargo</b> si los parámetros son modificados dentro del método, el cambio permanecerá sobre los valores originales incluso cuando el método termine.

Una reasignación al parámetro no tiene implicancias fuera del método ni del valor original (se entiende que el parámetro apunta a un nuevo valor).

```java
public void moveCircle(Circle circle, int deltaX, int deltaY) {
    // code to move origin of circle to x+deltaX, y+deltaY
    circle.setX(circle.getX() + deltaX);
    circle.setY(circle.getY() + deltaY);
        
    // code to assign a new reference to circle
    circle = new Circle(0, 0);
}
```

Si llamamos a éste método:

```java
// myCircle references to new memory space
Circle myCircle = new Circle(10, 20);
moveCircle(myCircle, 23, 56);

// After invoke: 
myCircle.getX(); // 33
myCircle.getY(); // 76
```
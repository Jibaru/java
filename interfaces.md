# [Interfaces](#interfaces)

Una interfaz en java es un tipo de referencia, similar a las clases, que puede contener constantes, signaturas de métodos, métodos por defecto, métodos static y tipos anidados.

El cuerpo de los métodos solo existe en los métodos por defecto y métodos static.

Las interfaces no pueden ser instanciadas, solo *implementadas* por una clase o *heredadas* por otras interfaces.

La declaración de una interfaz es similar a la una clase:

```java
public interface OperateCar {

   // constant declarations, if any

   // method signatures
   
   // An enum with values RIGHT, LEFT
   int turn(Direction direction,
            double radius,
            double startSpeed,
            double endSpeed);
   int changeLanes(Direction direction,
                   double startSpeed,
                   double endSpeed);
   int signalTurn(Direction direction,
                  boolean signalOn);
   int getRadarFront(double distanceToCar,
                     double speedOfCar);
   int getRadarRear(double distanceToCar,
                    double speedOfCar);
         ......
   // more method signatures
}
```

**Importante:** Los métodos no presentan `{}` puesto que son sólo signaturas.

Para usar una interfaz, escriba una clase que *implemente* la interfaz.


```java
public class OperateBMW760i implements OperateCar {

    // the OperateCar method signatures, with implementation --
    // for example:
    int signalTurn(Direction direction, boolean signalOn) {
       // code to turn BMW's LEFT turn indicator lights on
       // code to turn BMW's LEFT turn indicator lights off
       // code to turn BMW's RIGHT turn indicator lights on
       // code to turn BMW's RIGHT turn indicator lights off
    }

    // other members, as needed -- for example, helper classes not 
    // visible to clients of the interface
}
```

Es importante darse cuenta que cada clase implementará de manera diferente una interfaz.

## [Definiendo una interfaz](#defining-an-interface)

La declaración de una interfaz consiste de modificadores, la palabra `interface`, el nombre de la interfaz, una lista de interfaces de las cuales extiende y separadas por comas (si hubiera) y el cuerpo de la interfaz.

```java
public interface GroupedInterface extends Interface1, Interface2, Interface3 {

    // constant declarations
    
    // base of natural logarithms
    double E = 2.718282;
 
    // method signatures
    void doSomething (int i, double x);
    int doSomethingElse(String s);
}
```

**Nota:** El modificador public indica que la interfaz puede usarse por cualquier clase en cualquier paquete.

### [El cuerpo de la interfaz](#interface-body)

El cuerpo de la interfaz puede contener `métodos abstractos`, `métodos por defecto` y `métodos static`.

- Los **métodos abstractos** terminan en `;`.
- Los **métodos por defecto** están definidos por el modificador `default`.
- Los **métodos static** están definidos por el modificador `static`.

Todos estos métodos son `public` de manera implícita (por lo que se puede omitir).

Adicionalmente, una interfaz puede contener `valores constantes` que son implícitamente `public`, `static` y `final` (por lo que se pueden omitir esta palabras).

## [Implementando una interfaz](#implementing-an-interface)

Para implementar una interfaz use la palabra `implements` en la declaración de una clase. Es posible implementar más de una interfaz, las cuales irán separadas por comas. Por convención la palabra `implements` va después de `extends`.

```java
public interface Relatable {
        
    // this (object calling isLargerThan)
    // and other must be instances of 
    // the same class returns 1, 0, -1 
    // if this is greater than, 
    // equal to, or less than other
    public int isLargerThan(Relatable other);
}
```

Implementación:

```java
public class RectanglePlus 
    implements Relatable {
    public int width = 0;
    public int height = 0;
    public Point origin;

    // four constructors
    public RectanglePlus() {
        origin = new Point(0, 0);
    }
    public RectanglePlus(Point p) {
        origin = p;
    }
    public RectanglePlus(int w, int h) {
        origin = new Point(0, 0);
        width = w;
        height = h;
    }
    public RectanglePlus(Point p, int w, int h) {
        origin = p;
        width = w;
        height = h;
    }

    // a method for moving the rectangle
    public void move(int x, int y) {
        origin.x = x;
        origin.y = y;
    }

    // a method for computing
    // the area of the rectangle
    public int getArea() {
        return width * height;
    }
    
    // a method required to implement
    // the Relatable interface
    public int isLargerThan(Relatable other) {
        RectanglePlus otherRect 
            = (RectanglePlus)other;
        if (this.getArea() < otherRect.getArea())
            return -1;
        else if (this.getArea() > otherRect.getArea())
            return 1;
        else
            return 0;               
    }
}
```

**Nota:** Observe que en la implementación de la interfaz, el método `isLarguerThan` recibe un objeto de tipo `Relatable` y este es casteado a `RectanglePlus`. Si no fuese así, el compilador no podría entender de que tipo es el objeto y fallaría la compilación.

## [Usando una interfaz como un tipo](#using-an-interface-as-a-type)

Cuando defines una nueva interfaz, defines una nueva referencia a un tipo de dato. Puedes usar los nombres de las interfaces en cualquier lugar que uses otro tipo de dato. Si defines una variable de referencia cuyo tipo de dato es una interfaz, cualquier objeto que asignes debe cumplir que debe ser una instancia de la clase que implemente dicha interfaz.

```java
public Object findLargest(Object object1, Object object2) {
   Relatable obj1 = (Relatable)object1;
   Relatable obj2 = (Relatable)object2;
   if ((obj1).isLargerThan(obj2) > 0)
      return object1;
   else 
      return object2;
}
```

En el método `findLargest` funcionará siempre que object1 y object2 sean pertenezcan a clases que implementen la interfaz `Relatable`.

## [Evolucionando interfaces](#evolving-interfaces)

Si se quiere agregar funcionalidad (métodos) a una interfaz, puede que tenga problemas con clases que implementen dicha interfaz, puesto que tendría que implementar en todas las clases la nueva funcionalidad agregada.

Considere la siguiente interfaz:

```java
public interface DoIt {
   void doSomething(int i, double x);
   int doSomethingElse(String s);
}
```

Si se desea agregar un método más:

```java
public interface DoIt {

   void doSomething(int i, double x);
   int doSomethingElse(String s);
   boolean didItWork(int i, double x, String s);
   
}
```

En todas las clases que se implemente dicha interfaz habrá que implementar el nuevo método (que puede resultar engorroso).

Una opción sería crear una nueva interfaz que herede de la anterior y que el lugar donde se necesite implementar el nuevo método ahora la implemente.

```java
public interface DoItPlus extends DoIt {

   boolean didItWork(int i, double x, String s);
   
}
```

Otra alternativa es usar `métodos por defecto`:

```java
public interface DoIt {

   void doSomething(int i, double x);
   int doSomethingElse(String s);
   default boolean didItWork(int i, double x, String s) {
       // Method body 
   }
   
}
```

## [Métodos por defecto](#default-methods)

Proveen una forma de agregar nueva funcionalidad a interfaces, manteniendo la compatibilidad con código escrito para versiones anteriores de dichas interfaces.

```java
public interface TimeClient {
    void setTime(int hour, int minute, int second);
    void setDate(int day, int month, int year);
    void setDateAndTime(int day, int month, int year,
                               int hour, int minute, int second);
    LocalDateTime getLocalDateTime();
    
    static ZoneId getZoneId (String zoneString) {
        try {
            return ZoneId.of(zoneString);
        } catch (DateTimeException e) {
            System.err.println("Invalid time zone: " + zoneString +
                "; using default time zone instead.");
            return ZoneId.systemDefault();
        }
    }
        
    default ZonedDateTime getZonedDateTime(String zoneString) {
        return ZonedDateTime.of(getLocalDateTime(), getZoneId(zoneString));
    }
}
```

Note que la signatura del método está precedida por `default`. Además el método no es abstracto.

### [Extendiendo interfaces que contienen métodos por defecto](#extending-interfaces-that-contain-default-methods)

Cuando extiendas una interfaz que contenga métodos por defecto, tener en cuenta:

- El método por defecto se va a heredar.
- Redeclarar el método por defecto lo hace abstracto.
- Redefinir el método lo sobreescribe.

Por ejemplo, si se hereda de la interfaz anterior:

```java
public interface AnotherTimeClient extends TimeClient { }
```

Cualquier clase que implemente `AnotherTimeClient` tendrá la implementación del método `TimeClient.getZoneDateTime`.

Ahora, suponiendo que hace lo siguiente:

```java
public interface AbstractZoneTimeClient extends TimeClient {
    public ZonedDateTime getZonedDateTime(String zoneString);
}
```

Cualquier clase que implemente `AbstractZoneTimeClient` tendrá que implementar el método `getZonedDateTime`.

Finalmente, si redefine el método:

```java
public interface HandleInvalidTimeZoneClient extends TimeClient {
    default public ZonedDateTime getZonedDateTime(String zoneString) {
        try {
            return ZonedDateTime.of(getLocalDateTime(),ZoneId.of(zoneString)); 
        } catch (DateTimeException e) {
            System.err.println("Invalid zone ID: " + zoneString +
                "; using the default time zone instead.");
            return ZonedDateTime.of(getLocalDateTime(),ZoneId.systemDefault());
        }
    }
}
```

Cualquier clase que implemente `HandleInvalidTimeZoneClient` tendrá el método `getZonedDateTime` con una implementación por defecto y no tendrá que implementarlo.

## [Métodos Static](#static-methods)

En adición a los métodos por defecto, también puede definir `métodos static` en interfaces.

```java
public interface TimeClient {
    // ...
    static public ZoneId getZoneId (String zoneString) {
        try {
            return ZoneId.of(zoneString);
        } catch (DateTimeException e) {
            System.err.println("Invalid time zone: " + zoneString +
                "; using default time zone instead.");
            return ZoneId.systemDefault();
        }
    }

    default public ZonedDateTime getZonedDateTime(String zoneString) {
        return ZonedDateTime.of(getLocalDateTime(), getZoneId(zoneString));
    }    
}
```


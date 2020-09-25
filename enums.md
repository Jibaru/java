# Enums

Los tipos enumerados son un tipo especial de datos que habilitan un valor a un conjunto de constantes.

Para definir un nuevo tipo enumerado use la palabra `enum`:

```java
public enum Day {
	SUNDAY, MONDAY, TUESDAY, WEDNESDAY,
    THURSDAY, FRIDAY, SATURDAY
}
```

Use enumeraciones cuando requiera representar un grupo constante de constantes.

```java
public class EnumTest {
	Day day;

    public EnumTest(Day day) {
    	this.day = day;
    }

    public void tellItLikeIs() {
    	switch(day) {
        	case MONDAY: 
            	System.out.println("Mondays are bad.");
                break;
            case FRIDAY:
            	System.out.println("Fridays are better.");
                break;
            default:
            	System.out.println("Midweek days are so-so.");
                break;
        }
    }

    public static void main(String[] args){
    	EnumTest firstDay = new EnumTest(Day.WEDNESDAY);
        firstDay.tellItLikeIs();
    }
}
```

Los enum en java son muy poderosos puesto que en realidad definen una clase (llamada tipo enumerado), por lo que pueden admitir campos y métodos.

Todos los enum heredan implicitamente de `java.lang.Enum`. Cuando se crea un enum, adicionalmente son agregados nuevos métodos, tales como `values`, que devuelve un array de todas las constantes del enum.

```java
for(Planet p:Planet.values()) {
	System.out.println(p);
}
```

Es posible definir varios valores para una constante del enum:

```java
public enum Planet {
    MERCURY (3.303e+23, 2.4397e6),
    VENUS   (4.869e+24, 6.0518e6),
    EARTH   (5.976e+24, 6.37814e6),
    MARS    (6.421e+23, 3.3972e6),
    JUPITER (1.9e+27,   7.1492e7),
    SATURN  (5.688e+26, 6.0268e7),
    URANUS  (8.686e+25, 2.5559e7),
    NEPTUNE (1.024e+26, 2.4746e7);

    private final double mass;   // in kilograms
    private final double radius; // in meters
    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }
    private double mass() { return mass; }
    private double radius() { return radius; }

    // universal gravitational constant  (m3 kg-1 s-2)
    public static final double G = 6.67300E-11;

    double surfaceGravity() {
        return G * mass / (radius * radius);
    }
    double surfaceWeight(double otherMass) {
        return otherMass * surfaceGravity();
    }
    public static void main(String[] args) {
        if (args.length != 1) {
            System.err.println("Usage: java Planet <earth_weight>");
            System.exit(-1);
        }
        double earthWeight = Double.parseDouble(args[0]);
        double mass = earthWeight/EARTH.surfaceGravity();
        for (Planet p : Planet.values())
           System.out.printf("Your weight on %s is %f%n",
                             p, p.surfaceWeight(mass));
    }
}
```
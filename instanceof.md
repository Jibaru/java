# [Instanceof](#instanceof)

Nos permite saber el tipo de instancia que almacena una variable o referencia.

## Ejemplo

Si creamos un `String` y comprobamos si el valor de la instancia creada es de este tipo.

```java
String texto = new String("Ignacio");
System.out.println(texto instanceof String); // true
```

Si tenemos una estructura de clases:

```java
public class Persona {}

class Alumno extends Persona {}
```
Podemos comprobar si la variable contiene una instancia de Persona:

```java
Persona p = new Persona();
System.out.println(p instanceof Persona); // true
```
Si una variable apunta a una instancia de una subclase, `instanceof` devolverá `true`:

```java
Persona q = new Alumno();
System.out.println(q instanceof Persona); // true
System.out.println(q instanceof Alumno); // true
```
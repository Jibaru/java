# [Anotaciones](#annotations)

## [Formato](#format-of-annotations)

Una anotación luce de la siguiente manera:

```java
@Entity
```

El caracter `@` le indica al compilador que lo que viene es una anotación.

Una anotación puede incluir elementos, nombrados o no nombrados, y también pueden poseer valores:

```java
@Author(
   name = "Benjamin Franklin",
   date = "3/27/2003"
)
class MyClass() { ... }
```

o también:

```java
@SuppressWarnings(value = "unchecked")
void myMethod() { ... }
```

Si la anotación solo posee un elemento llamado `value` se puede omitir este:

```java
@SuppressWarnings("unchecked")
void myMethod() { ... }
```

Si la anotación no posee elementos, los paréntesis pueden omitirse:

```java
@Override
void myMethod() { ... }
```

Es posible escribir múltiples anotaciones para una misma declaración:

```java
@Author(name = "Jane Doe")
@EBook
class MyClass { ... }
```

Si estas anotaciones tienen el mismo tipo, se les llama anotaciones repetidas:

```java
@Author(name = "Jane Doe")
@Author(name = "John Smith")
class MyClass { ... }
```

Los tipos de anotaciones son aquellos definidos en los paquetes `java.lang` o `java.lang.annotation` del API de Java, sin embargo es posible definir anotaciones personalizadas.

## [Donde usar anotaciones](#where-annotations-can-be-used)

Se puede usar anotaciones en:

- Declaraciones de clases
- Declaraciones de campos
- Declaraciones de métodos
- Declaraciones de cualquier otro elemento.

Cuando es usada en una declaración, la anotación aparece (por convención) en la misma línea.

A partir de java SE 8 es posible usar anotaciones en el uso de tipos, llamadas `anotaciones de tipo`, como:

- Creación de una instancia

```java
new @Interned MyObject();
```

- Casteos

```java
myString = (@NonNull String) str;
```

- En implementaciones:

```java
class UnmodifiableList<T> implements
    @Readonly List<@Readonly T> { ... }
```

- En declaraciones de lanzamiento de excepciones:

```java
void monitorTemperature() throws
    @Critical TemperatureException { ... }
```

## [Declaración de una anotación](#declaring-an-annotation-type)

Suponga que usa el tradicional comentario al inicio de cada clase para proveer de información importante:

```java
public class Generation3List extends Generation2List {

   // Author: John Doe
   // Date: 3/17/2002
   // Current revision: 6
   // Last modified: 4/12/2004
   // By: Jane Doe
   // Reviewers: Alice, Bill, Cindy

   // class code goes here

}
```

Para añadir esta información con una anotación, primero defina el tipo de la anotación:

```java
@interface ClassPreamble {
   String author();
   String date();
   int currentRevision() default 1;
   String lastModified() default "N/A";
   String lastModifiedBy() default "N/A";
   // Note use of array
   String[] reviewers();
}
```

La definición luce similar a la definición de una interfaz, donde la palabra `interface` es precedida por un `@` (significa AT = `annotation type`). El cuerpo de contiene los elementos de la anotación (similares a métodos) y pueden tener valores por defecto.

Una vez definida la anotación es posible usarla.

```java
@ClassPreamble (
   author = "John Doe",
   date = "3/17/2002",
   currentRevision = 6,
   lastModified = "4/12/2004",
   lastModifiedBy = "Jane Doe",
   // Note array notation
   reviewers = {"Alice", "Bob", "Cindy"}
)
public class Generation3List extends Generation2List {

// class code goes here

}
```

**Nota:** Para hacer visible la información de la nueva anotación creada en la documentación generada por `java-doc` agrega `@Documented`:

```java
// import this to use @Documented
import java.lang.annotation.*;

@Documented
@interface ClassPreamble {

   // Annotation element definitions
   
}
```

## [Anotaciones predefinidas](#predefined-annotations-types)

### [Anotaciones usadas por el lenguaje java](#annotation-types-used-by-java-language)

- `@Deprecated`: Indica que el elemento está descontinuado y no debe ser usado más. El compilador genera una advertencia cuando se usa un elemento marcado con esta anotación.

```java
// Javadoc comment follows
/**
    * @deprecated
    * explanation of why it was deprecated
    */
@Deprecated
static void deprecatedMethod() { }
```

- `@Override`: Indica al compilador que un elemento va a ser sobreescrito por otro otro elemento en la superclase. 

```java
// mark method as a superclass method
// that has been overridden
@Override 
int overriddenMethod() { }
```

- `@SupressWarnings`: Le dice al compilador que no genere una advertencia en concreto.

```java
// use a deprecated method and tell 
// compiler not to generate a warning
@SuppressWarnings("deprecation")
void useDeprecatedMethod() {
    // deprecation warning
    // - suppressed
    objectOne.deprecatedMethod();
}
```

Existen dos categorias de advertencias: `unchecked`, que puede ocurrir al interactuar con código heredado escrito antes de la llegada de los genéricos, y `deprecation`, que indica que se está ejecutando un elemento marcado con `@Deprecated`.

Para no generar múltiples categorías de advertencias use la siguiente sintaxis:

```java
@SuppressWarnings({"unchecked", "deprecation"})
```

- `@SafeVarargs`: Cuando se aplica a un método o constructor, se asegura de que el código no ejecute operaciones potencialmente inseguras usando el parámetro `varargs`. Cuando se usa esta anotación, advertencias unchecked hacia varargs son no tomadas en cuenta.

- `@FunctionalInterface`: Indica que el tipo de la declaración es una interfaz funcional.

### [Anotaciones para aplicar a otras anotaciones](#annotations-that-apply-to-other-annotations)

Son llamadas meta-anotaciones. Está definidas en `java.lang.annotation`.

- `@Retention`: Especifica como se guarda la anotación marcada:
  - RetentionPolicy.SOURCE: La anotación marcada es solo retenida en el nivel de origen y es ignorada por el compilador.
  - RetentionPolicy.CLASS: La anotación marcada es retenida por el compilador en tiempo de compilación, pero es ignorada por la JVM.
  - RetentionPolicy.RUNTIME: La anotación marcada es retenida por la JVM y solo puede ser usada por el entorno de ejecución.

- `@Documented`: Indica que siempre que se use la anotación marcada, sus elementos deben documentarse con la java-doc.

- `@Target`: Marca a otra anotación para restringir a que tipos de elementos de java puede aplicarse, y estos pueden ser:

  - ElementType.ANNOTATION_TYPE: Puede aplicarse a una anotación de tipo.
  - ElementType.CONSTRUCTOR: Puede aplicarse a un constructor.
  - ElementType.FIELD: Puede aplicarse a un campo.
  - ElementType.LOCAL_VARIABLE: Puede aplicarse a una variable local.
  - ElementType.METHOD: Puede aplicarse a un método.
  - ElementType.PACKAGE: Puede aplicarse a una declaración de un paquete.
  - ElementType.PARAMETER: Puede aplicarse a los parámetros de un método.
  - ElementType.TYPE: Puede aplicarse a cualquier elemento de un clase.

- `@Inherited`: Indica que la anotación marcada puede heredar de una superclase (Por defecto no es cierto). Solo es posible aplicarse a declaraciones de clases.

- `@Repeatable`: Indica que la anotación marcada puede aplicarse más de una vez a la misma declaración de tipo donde es usada.

## [Anotaciones de tipo y Pluggable Type System](#type-annotations-and-pluggable-type-system)

Las anotaciones de tipo fueron creadas con la finalidad de proveer análisis para los tipos en java. Java no cuenta con un framework de type checking, pero es posible alojar uno gracias a su sistema. 

Por ejemplo, si quieres que un tipo de variable particular nunca sea asignado a `null`, puedes evadir esto desencadenando un `NullPointerException`. Para ello es posible crear un plug-in para checkear:

```java
@NonNull String str;
```

Cuando compile el código, incluyendo `NonNull` en la línea de comandos, el compilador mostrará las advertencias si detecta un problema , proveendo la capacidad de poder modificar el código para corregir dichos problemas.

Puede usar [el framework checker](https://checkerframework.org/) si no desea escribir un plug.
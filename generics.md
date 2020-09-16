# Genéricos

A través de los genéricos es posible implementar una clase que acepten varios tipos de datos si es que éstos pueden realizar operaciones similares.

## Operador Diamante

El operador `<T>` con T representando el tipo de dato, nos permite generalizar el tipo de dato con el que va a funcionar una clase o instancia.

## Sintaxis

La sintaxis es la siguiente:

```java
public class Clase <T> {

    private T objetoGenerico;

    public Clase(T objeto) {
        this.objeto = objeto;
    }

    public void mostrarTipo() {
        System.out.println("T es un: " + objeto.getClassName);
    }
}
```

Si creamos una instancia de esta clase y mostramos el tipo:

```java
Clase<String> a = new Clase<String>();
Clase<Integer> b = new Clase<Integer>();

a.mostrarTipo(); // String
b.mostrarTipo(); // Integer
```

## Convenciones

La representación de los tipos sigue una convención:

| Nomenclatura  | Representación    |
| :-----------: | ----------------- |
| E             | Elemento          |
| K             | Llave             |
| N             | Número            |
| T             | Tipo              |
| V             | Valor             |
| S,U,V         | Tipos 2º, 3º y 4º |

## Seguridad en los tipos (type-safety)

Indican que los tipos aceptados solo serán los definidos en 

```java
List<String> lista = new ArrayList<>();
lista.add("Ignacio");
lista.add(25); // Ok
```

## Evitar casteos

Si tenemos elementos T que van a ser obtenidos de una instancia genérica, no es necesario realizar un casteo.

```java
String nombre = lista.get(0); // No es necesario (String)
```

## Clases Genéricas multitipo

Podemos establecer múltiples tipos genéricos para una clase genérica.

```java
public class ClaseGenerica <T, K, V, U, S> { /* ... */ }
```

Y al instanciar, de la misma forma que con un dato genérico, lo haremos pasando el tipo de dato correspondiente y de forma ordenada.

```java
ClaseGenerica<String, Integer, Float, Double, Clase> c = new ClaseGenerica<>();
```

A su vez, es posible ingresar Clases genéricas como tipos a otras clases genéricas:

```java
List<Clase<String>> listaGen = new ArrayList<>();
```

## WildCards

Es posible parametrizar los tipos genéricos usando el operador  `?` (o wildcard).

### Parametrización UnBounded

Usando únicamente el operador `?` decimos que el tipo genérico puede recibir cualquier tipo de dato (en general, Object):

```java
// obj será de tipo ClaseGen<Object> por defecto
public void algunMetodo(ClaseGen<?> obj) { }
```

## Parametrización UpperBounded
Si usamos `extends` podremos decirle al tipo que necesariamente tiene que heredar o implementar de otra clase o interfaz.

```java
// obj será de tipo Clase<Object> por defecto
public void algunMetodo(ClaseGen<? extends OtraClaseOInterfaz> obj) { }
```

## Parametrización LowerBounded
Si usamos `super` podremos decirle al tipo que necesariamente tiene que ser una superclase de otra clase.

```java
// obj será de tipo Clase<Object> por defecto
public void algunMetodo(ClaseGen<? super ClaseHija> obj) { }
```


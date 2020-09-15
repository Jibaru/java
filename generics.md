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


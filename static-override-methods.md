# [Static](#static)

La palabra reservada static permite acceder a miembros de la clase. 

# [Sobreescritura de métodos](#override-methods)

Es posible sobreescribir métodos heredados en una clase.

Un método de instancia no puede ser sobreescrito como un método de clase y viceversa.

Se recomienda utilizar la anotación `@override` al momento de sobreescribir una clase;

## Ejemplo: 
Suponga que tiene dos clases: Persona y Alumno, donde la relación de herencia es: Alumno extiende a Persona.
Además, la clase Persona tiene el método de instancia sumar y el método de clase restar.

```java
// Clase Persona
public class Persona {

    public int sumar(int numero) {
        return numero + 1;
    }

    public static int restar(int numero) {
        return numero - 1;
    }

}
```

Al heredar los métodos y sobreescribirlos, ahora se tomarán los valores determinados por la clase Alumno y no por los de la clase Persona.

```java
// Clase Persona
public class Alumno extends Persona {

    // Sobreescritura de métodos de instancia
    @override
    public int sumar(int numero) {
        return numero + 2;
    }

    // Sobreescritura de métodos de clase
    @override
    public static int restar(int numero) {
        return numero - 2;
    }
}
```

Si realizamos las comprobaciones:
```java

public class App {

    public static void main(String[] args) {
        
        Alumno a = new Alumno();
        Persona p = new Persona();
        Persona q = new Alumno();

        System.out.println(a.sumar(5)); // 7
        System.out.println(Alumno.restar(9)); // 7
        System.out.println(p.sumar(5)); // 6
        System.out.println(Persona.restar(9)); // 8
        System.out.println(q.sumar(5)); // 7

    }

}

```
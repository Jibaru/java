# [Clases anidadas](#nested-classes)

En java es posible alojar una clase dentro de otra clase. A éste tipo de clases se les conoce como `clases anidadas`.

```java
class OuterClass {
    ...
    class NestedClass {
        ...
    }
}
```

Existen dos tipos de clases anidadas.

- Las clases anidadas declaradas con `static` son llamadas `clases anidadas static`.
- La clases sin `static` son llamadas `clases internas`.

```java
class OuterClass {
    ...
    static class StaticNestedClass {
        ...
    }
    class InnerClass {
        ...
    }
}
```

Una clase anidada se considera un miembro de la clase. 
Una clase interna tiene acceso a los miembros de la clase que la encierra, incluso si estos miembros son `private`.
Una clase anidada static no tiene acceso a los miembros de la clase que la encierra.

Una clase anidada pueder tener modificadores de acceso como si fuera un miembro más (a diferencia de la clase que la encierra que solo puede ser `public` o `privada al paquete`, la clase anidada puede ser `public`, `private` o `protected`).

## [¿Por qué usar clases anidadas?](#why-use-nested-classes)

- Para agrupar lógicamente clases que solo se usan en un `único lugar`. Por ejemplo si la clase `A` solo se usa en la clase `B` es lógico anidar `A` dentro de `B`.
- Incrementa la encapsulación. Si tenemos dos clases, `A` y `B`, necesitando esta última de poder acceder a los miembros privados de `A`, si la clase `B` se hace anidada en `A` podrá lograrlo.
- Mantiene el código más legible y mantenible.

## [Clases anidadas static](#static-nested-classes)

De la misma forma que los métodos static, este tipo de clases no puede acceder a variables ni métodos de instancia sin una referencia.

Para acceder a estas clases use la siguiente sintaxis:

```java
OuterClass.StaticNestedClass
```

## [Clases internas](#inner-classes)

Estas clases si pueden acceder a miembros y métodos de instancia, sin embargo no pueden definir ningún miembro static por si mismas.

Una instancia de la clase interna solo puede existir si existe un instancia de la clase que la encierra.

Para instanciar una clase interna, primero instancie un objeto de la clase que la encierra, luego con el objeto creado use la siguiente sintaxis:

```java
OuterClass.InnerClass innerObject = outerObject.new InnerClass();
```

Existen dos tipos de clases internas: `clases locales` y `clases anónimas`.

## [Shadowing](#shadowing)

Si se declara una variable (miembro o parámetro) en un área particular (en una clase interna o en la definición de un método) que posea el mismo nombre de otra declaración que encierra dicha área, la nueva declaración `ensombrece` la anterior.

```java
public class ShadowTest {

    public int x = 0;

    class FirstLevel {

        public int x = 1;

        void methodInFirstLevel(int x) {
            System.out.println("x = " + x);
            System.out.println("this.x = " + this.x);
            System.out.println("ShadowTest.this.x = " + ShadowTest.this.x);
        }
    }

    public static void main(String... args) {
        ShadowTest st = new ShadowTest();
        ShadowTest.FirstLevel fl = st.new FirstLevel();
        fl.methodInFirstLevel(23);
    }
}
// Output:
// x = 23
// this.x = 1
// ShadowTest.this.x = 0
```
 
Use `this` para referirse a un miembro de la clase en donde se está:

```java
System.out.println("this.x = " + this.x);
```

Para acceder a miembros con mayor alcance use el nombre de la clase:

```java
System.out.println("ShadowTest.this.x = " + ShadowTest.this.x);
```

## [Serialización](#serialization)

No se recomienda serializar clases internas. Cuando el compilador de java compila los constructores de las clases internas crea `construcciones sintéticas`. Estas construcciones permiten a los compiladores implementar nuevas funciones del lenguaje java sin cambios en la JVM. 

## [Clases locales](#local-classes)

Son clases que se encuentran definidas en un bloque, entre una o más sentencias. Se suelen ver definidas dentro del cuerpo de un método.

### [Declaración de clases locales](#declaring-local-classes)

Es posible declarar una clase local en cualquier bloque (cuerpos de métodos, de for, de if).

```java
public class MyClass {

    public static void method() {

        class LocalClass {

        }

    }
}
```

### [Acceder a los miembros de la clase que la encierra](#accesing-members-of-an-enclosing-class)

Una clase local tiene acceso a los miembros de la clase que la encierra. Para acceder a dichos miembros use la siguiente sintaxis:

```java
EnclosingClass.member
```

Adicionalmente una clase local puede acceder a las variables locales siempre que hallan sido declaradas `final`. También es posible acceder a variables locales no finales si su valor no se cambia en la clase local, a esas variables se les conoce como `efectivamente final`.

### [Aspectos importantes de las clases locales](#important-concepts-of-local-classes)

- Las clases locales no pueden definir ningún miembro `static`.
- Las clases locales en métodos static solo pueden referirse a miembros static de la clase que las encierra.
- Las clases locales no pueden ser `static`.
- No existen <i> interfaces locales </i>, éstas son siempre `static`.

## [Clases anónimas](#anonymous-classes)

Una clase anónima es una expresión. La sintaxis es similar a la invoación de un constructor, sólo que en esta se define la clase en un bloque:

```java
HelloWorld frenchGreeting = new HelloWorld() {
    String name = "tout le monde";
    public void greet() {
        greetSomeone("tout le monde");
    }
    public void greetSomeone(String someone) {
        name = someone;
        System.out.println("Salut " + name);
    }
};
```

La expresión consiste de:

- El operador `new`
- El nombre de la `interface` a implementar o `clase` a extender.
- Paréntesis, que contiene argumentos al constructor (solo para clases, cuando se implementa una interfaz se dejan vacíos).
- El cuerpo de la clase.

### [Accediendo a variables locales, declarando y accediendo a miembros de la clase anónima](#accessing-local-variables-of-the-enclosing-scope,-and-declaring-and-accessing-members-of-the-anonymous-class)

Una clase anónima:

- Puede acceder a los miembros de la clase que la encierra.
- No puede acceder a variables locales de fuera que no sean `final` o `efectivamente final`.
- Igual que en las clases anidadas, la declaración de un tipo `ensombrece` otras declaraciones de fuera con el mismo nombre.
- No puede tener `inicializadores static` o `interfaces miembro`.
- Puede tener `miembros static` siempre que sean `constantes`.
- Puede tener: `campos`, `métodos extra`, `inicializadores de variables de instancia`, `clases locales`.
- No es posible declarar constructores.

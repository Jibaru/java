# [Expresiones Lambda](#lambda-expressions)

Al momento de crear `clases anónimas` que contienen un solo método puede ser engorroso tener que declarar toda una expresión significativamente grande. Las `lambdas` proveen una forma de expresar instancias de una clase con un único método de forma más compacta.

## [Sintaxis de las expresiones lambda](#syntax-of-lambda-expressions)

- En paréntesis, la lista de parámetros separados por comas. Si solo hay un parámetro se pueden omitir los paréntesis. El tipo de dato de los parámetros también se puede omitir.
- El símbolo de flecha `->`
- El cuerpo, que consiste en una expresión o un bloque de sentencias (si se usa esto último es posible usar `return`).

```java
(arguments) -> expression
```

```java
singleArgument -> { return expression; }
```

```java
public class Calculator {
  
    interface IntegerMath {
        int operation(int a, int b);   
    }
  
    public int operateBinary(int a, int b, IntegerMath op) {
        return op.operation(a, b);
    }
 
    public static void main(String... args) {
    
        Calculator myApp = new Calculator();
        IntegerMath addition = (a, b) -> a + b;
        IntegerMath subtraction = (a, b) -> a - b;
        System.out.println("40 + 2 = " +
            myApp.operateBinary(40, 2, addition));
        System.out.println("20 - 10 = " +
            myApp.operateBinary(20, 10, subtraction));    
    }
}
```

## [Acceso a variables del scope que los encierra](#accesing-local-variables-of-the-enclosing-scope)

Las lambda pueden acceder a variables locales, sin embargo estas no pueden contener ninguna declaración de variable que `ensombrezca` a las de fuera, es decir, no pueden tener el mismo nombre. Por norma, las lambda no agregan un nuevo nivel al scope.

```java
import java.util.function.Consumer;

public class LambdaScopeTest {

    public int x = 0;

    class FirstLevel {

        public int x = 1;

        void methodInFirstLevel(int x) {
            
            // The following statement causes the compiler to generate
            // the error "local variables referenced from a lambda expression
            // must be final or effectively final" in statement A:
            //
            // x = 99;
            
            Consumer<Integer> myConsumer = (y) -> 
            {
                System.out.println("x = " + x); // Statement A
                System.out.println("y = " + y);
                System.out.println("this.x = " + this.x);
                System.out.println("LambdaScopeTest.this.x = " +
                    LambdaScopeTest.this.x);
            };

            myConsumer.accept(x);

        }
    }

    public static void main(String... args) {
        LambdaScopeTest st = new LambdaScopeTest();
        LambdaScopeTest.FirstLevel fl = st.new FirstLevel();
        fl.methodInFirstLevel(23);
    }
}
```

De la misma forma que las `clases anónimas`, las lambda solo pueden acceder a las variables locales o miembros siempre que estos sean `final` o `efectivamente final`.

## [Target type](#target-typing)

Para que el compilador pueda saber el tipo que tendrá una lambda usa el `target tipe`:

```java
public void printPersonsWithPredicate(List<Person> roster, Predicate<Person> tester)
```

Por ejemplo, la función `printPersonsWithPredicate` espera como segundo parámetro un `Predicate<Person>`, por lo que la lambda que sea pasada allí será de dicho tipo.

Solo es posible crear expresiones lambda cuando se pueda determinar el `target type`, es decir solo en:

- Declaraciones de variables
- Asignaciones
- Sentencias de retorno
- Inicializaciones de arreglos
- Como argumentos en métodos o constructores
- En cuerpos de una expresión lambda
- En expresiones condicionales `?:`
- En expresiones de casteo

## [Target types y argumentos de métodos](#target-types-and-methods-arguments)

Para los argumentos de un método, el compilador interpreta el `target type` tomando en cuenta:

- Resolución de sobrecargas
- Inferencia del tipo del argumento

Por ejemplo, suponga que tiene lo siguiente:

```java
public interface Runnable {
    void run();
}

public interface Callable<V> {
    V call();
}
```

El método `run` no posee ningún tipo, sin embargo `call` si posee.

Si se tienen métodos sobrecargados:

```java
void invoke(Runnable r) {
    r.run();
}

<T> T invoke(Callable<T> c) {
    return c.call();
}
```

Y se llama a alguno de ellos usando una expresión lambda:

```java
String s = invoke(() -> "done");
```

El método al cual se está llamando es a `invoke(Callable<T>)` porque éste retorna un valor, a diferencia de `ìnvoke(Runnable)`. Para este caso el tipo de la lambda es `Callable<T>`.

## [Serialización](#serialization)

Es posible serializar una lambda si su `target type` y los argumentos que posea son serializables, sin embargo, no se recomienda serializar lambdas. 

## [Referencias a métodos](#method-references)

A veces una lambda no hace nada más que llamar a un método. Para estas situaciones existe una forma más compacta de realizar dicha llamada.

Por ejemplo al implementar una lambda para una comparación:

```java
Arrays.sort(rosterAsArray,
    (a, b) -> Person.compareByAge(a, b)
);
```

Como la expresión lambda solo invoca a un método, es posible escribirla como una referencia a un método:

```java
Arrays.sort(rosterAsArray, Person::compareByAge);
```

Escribir `Person::compareByAge` es lo mismo a  `(a, b) -> Person.compareByAge(a, b)`. Aquí suceden dos cosas:

- La lista de parámetros es copiada de `Comparator<Person>.compare`, es decir `(Person, Person)`.
- El cuerpo llama al método `Person.compareByAge`.

### [Tipos de referencias a métodos](#kinds-of-a-method-references)

Existe 4 formas de referirse a métodos:

| Forma | Ejemplo |
| ------ | :------: |
| Ref. a un método static | ContainingClass::staticMethodName | 
| Ref. a un método de instancia de un objeto | containingObject::instanceMethodName |
| Ref. a un método de instancia de un objeto arbitrario de un tipo en concreto | ContainingType::methodName |
| Ref. a un constructor | ClassName::new |

Ejemplos: 

<b>Ref. a un método static:</b>
```java
Arrays.sort(rosterAsArray, Person::compareByAge);
```

<b>Ref. a un método de instancia de un objeto:</b>
```java
ComparisonProvider myComparisonProvider = new ComparisonProvider();
Arrays.sort(rosterAsArray, myComparisonProvider::compareByName);
```

<b>Ref. a un método de instancia de un objeto arbitrario de un tipo en concreto: </b>
```java
String[] stringArray = { "Barbara", "James", "Mary", "John",
    "Patricia", "Robert", "Michael", "Linda" };
Arrays.sort(stringArray, String::compareToIgnoreCase);
// (String a, String b) -> a.compareToIgnoreCase(b)
```

<b>Ref. a un constructor:</b>
```java
Set<Person> rosterSet = transferElements(roster, HashSet::new);
// Set<Person> rosterSetLambda =
//   transferElements(roster, () -> { return new HashSet<>(); });
```
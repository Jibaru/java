# Expresiones, declaraciones y bloques

## Expresiones

Son construidos a partir de variables, operadores y llamadas a métodos.

```java
1 * 2 * 3
x + y / 2 // Ambiguo, se interpretaría como: x  + (y / 2)
(x + y) / 2 // No ambiguo, recomendado
```

## Sentencias

Son similares a las sentencias en lenguajes naturales. Todas terminan con `;`.
Son sentencias de expresión:

- Expresiones de asignación
- Usar `++` o `--`
- Invocaciones a métodos
- Creación de objetos

```java
// assignment statement
aValue = 8933.234;
// increment statement
aValue++;
// method invocation statement
System.out.println("Hello World!");
// object creation statement
Bicycle myBike = new Bicycle();
```

Son sentencias de declaración:

- La declaración de una variable

```java
double aValue = 8933.234;
```

Son sentencias de control de flujo aquellas que controlan el orden de ejecución. Para más detalles revisar [Sentencias de control de flujo](control-flow-statements.md).

## Bloques

Un bloque es un grupo de cero o más sentencias delimitadas por llaves `{}`.

```java
boolean condition = true;
if (condition) { // begin block 1
    System.out.println("Condition is true.");
} // end block one
else { // begin block 2
    System.out.println("Condition is false.");
} // end block 2
```
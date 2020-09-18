# [Operadores](#operators)

Son símbolos especiales que permiten realizar operaciones con uno o más operandos para devolver un resultado.

En java hay operaciones que preceden a otras. La siguiente tabla muestra la precedencia de cada operador.

Nota: Todos los operadores binarios (menos el de asignación) se evaluan de izquierda a derecha.
Nota: Todos los operadores de asignación se evalúan de derecha a izquierda.

| Operadores          | Precedencia (Más arriba, mayor precedencia) |
| ------------------- | :------------------------------------------:|
|sufijo               |	expr++ expr--                               |
|unario               |	++expr --expr +expr -expr ~ !               |
|multiplicativo	      |* / %                                        |
|additivo             |	+ -                                         |
|shift                |	<< >> >>>                                   |
|relacional           |	< > <= >= instanceof                        |
|es igual             |	== !=                                       |
|bitwise AND          |	&                                           |
|bitwise exclusive OR |	^                                           |
|bitwise inclusive OR |	\|                                          |
|lógico AND           |	&&                                          |
|lógico OR            |	\|\|                                        |
|ternario             |	? :                                         |
|asignación           |	= += -= *= /= %= &= ^= |= <<= >>= >>>=      |

## [Operador de asignación](#assignment-operator)

Asigna el valor de la dereacha al operando de la izquierda.
También sirve para asignar `referencias a objetos`.

```java
int cadence = 0;
int speed = 0;
int gear = 1;
```

## [Operadores aritméticos](#arithmetics-operators)

Los operadores de suma `+`, resta `-`, división `/`, multiplicación `*`, concatenación `+` (solo con `String`) y módulo (o residuo) `%`.

```java
int result = 1 + 2; // 3
result = result - 1; // 2
result = result * 2; // 4
result = result / 2; // 2
result = result + 8; // 10
result = result % 7; // 3

String firstString = "This is";
String secondString = " a concatenated string.";
System.out.println(firstString+secondString);
```

## [Operadores Unarios](#unary-operators)

Solo requieren de un operando. Tenemos el operador para indicar un número positivo `+`, un número negativo `-`, incrementar en 1 `++`, decrementar en 1 `--`, invertir valor de un boolean `!`.

```java
int result = +1; // 1
result--; // 0
result++; // 1
result = -result; // -1
boolean success = false; // false
success = !success; // true
```

El operador de incremento y decremento pueden aplicarse antes o después del operando. Normalmente no tiene ninguna implicación, pero en operaciones grandes puede ser significativo.

```java
int i = 3;
i++;
System.out.println(i); // 4
++i;			   
System.out.println(i); // 5
System.out.println(++i); // 6
System.out.println(i++); // 6
System.out.println(i); // 7
```

## [Operadores de comparación y relacionales](#equality-and-relationals-operators)

Indican si un valor es mayor, menor, igual o diferente de otro. Tenemos el operador es igual `==`, no es igual `!=`, mayor a `>`, menor a `<`, mayor o igual a `>=`, menor o igual a `<=`.

```java
int value1 = 1;
int value2 = 2;
if(value1 == value2)
    System.out.println("value1 == value2");
if(value1 != value2)
    System.out.println("value1 != value2");
if(value1 > value2)
    System.out.println("value1 > value2");
if(value1 < value2)
    System.out.println("value1 < value2");
if(value1 <= value2)
    System.out.println("value1 <= value2");
```

## [Operadores condicionales](#conditional-operators)

Indican condiciones booleanas. Tenemos el condicional AND `&&` y el condicional OR `||`

```java
int value1 = 1;
int value2 = 2;
if((value1 == 1) && (value2 == 2))
    System.out.println("value1 is 1 AND value2 is 2");
if((value1 == 1) || (value2 == 1))
    System.out.println("value1 is 1 OR value2 is 1");
```

También existe el operador ternario que es una forma corta de expresar una sentencia if-else-then. 

```java
int val1 = 1;
int val2 = 2;
int res;
boolean condicion = true;

res = condicion ? val1 : val2;

System.out.println(res); // 1
```

## [Operador de comparación de tipos (instanceof)](#type-comparison-operator-instanceof)

Compara si un objeto pertenece a algún tipo.

Devuelve `true` si el objeto comparado es una instancia de una clase, subclase o implementa alguna interfaz.

**Nota:** Recordar que `null` no es una instancia de algo.

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

## [Operadores Bitwise y Bit shift](#bitwise-and-bit-shift-operators)

El operador `~` invierte un patrón de bits.
El operador `<<` mueve un patrón de bits hacia la izquierda, y el operador `>>` hacia la derecha.
El operador `>>>` mueve un cero en la posición más a la izquierda.
El operador `&` realiza la operación AND.
El operador `|` realiza la operación OR inclusiva.
El operador `^` realiza la operación OR exclusiva.

```java
int bitmask = 0x000F;
int val = 0x2222;
System.out.println(val & bitmask); // 2
```
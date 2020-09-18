# [Tipos de dato](#data-types)

Los tipos de datos primitivos:

## [Byte (byte)](#byte)

De 8 bits, valores desde -128 hasta 127 (incluyendo).

## [Short (short)](#short)

De 16 bits, valores desde -32,768 hasta 32,767 (incluyendo).

## [Int (int)](#int)

De 32 bits, valores de -2<sup>31</sup> hasta 2<sup>31</sup> - 1 (incluyendo). Se puede usar la clase Integer para representar valores unsigned.

## [Long (long)](#long)

De 64 bits, valores de -2<sup>63</sup> hasta 2<sup>63</sup> - 1 (incluyendo). Se puede usar la clase Long para representar valores unsigned.

## [Float (float)](#float)

Precisión de punto flotante 32-bit IEEE 754.

## [Double (double)](#double)

Precisión de punto flotante 64-bit IEEE 754.

## [Boolean (boolean)](#boolean)

Representan 1 bit de información. Dos posibles valores: `true` o `false`.

## [Char (char)](#char)

Un único caracter Unicode de 16 bits. Valores desde '\u0000' (0) hasta '\uffff' (65,535, incluyendo). 

Adicionalmente java provee de la clase `java.lang.String` para el manejo de cadenas de caracteres. Todos los String son `inmutables`.

# [Valores por defecto](#default-values)

Solo se aplican valores por defecto a atributos de una clase. Para variables locales dará un error en tiempo de compilación.

Los valores por defecto para los tipos de datos primitivos, incluyendo String:

| Tipo de dato | Valor por defecto |
|--------------|:-----------------:|
| byte         | 0                 |
| short        | 0                 |
| int          | 0                 |
| long         | 0L                |
| float        | 0.0f              |
| double       | 0.0d              |
| char         | '\u00000'         |
| String (u otro objeto)| null     |
| boolean      | false             |

# [Literales](#literals)

Un literal en una representación de un valor.

```java
boolean result = true;
char capitalC = 'C';
byte b = 100;
short s = 1000;
int i = 10000;
```

## [Literales enteros](#integers-literals)

Para los long se puede usar la terminación `L`.
Los enteros pueden representarse como: decimales, hexadecimales, binarios.

```java
int decVal = 26; // 26
int hexVal = 0x1a; // 26
int binVal = 0b11010; // 26
```

## [Literales flotantes](#floating-point-literals)

Pueden terminar con `F`. Opcionalmente con `D`.
Los flotantes pueden representarse como: notación científica (usando `E`), F (32 bits), D (64 Bits, se suele omitir la `D`).

```java
double d1 = 123.4;
double d2 = 1.234e2;
float f1 = 123.4f;
```

## [Literales de caracter y String](#characters-and-string-literals)

Pueden contener cualquier caracter Unicode UTF-16.
Para caracteres se usar comillas simples `''`.
Para String se utilizan comillas dobles `""`.
Se pueden escapar backspaces `\b`, tabs `\t`, salto de línea `\n`, salto de form `\f`, retorno `\r`, comillas `\'` y `\"`, backslash `\\`.

Para los String concretamente se puede usar el literal `null` que indica que no ha sido inicializado.

También hay literales de clase, por ejemplo, para los String puede usar `String.class`. Esto devolvería un objeto de tipo `Class` que simboliza el tipo de la clase String.

## [Guiones bajo en literales numéricos](#underscore_numerics)

Principalmente para dar un mejor acabado a un literal numérico. Solo se debe respetar que:
- No pueden ir al `inicio` o `final` de un número.
- No pueden ir cerca de un `.` decimal.
- No pueden ir cerca de un sufijo `F` o `L`.
- No pueden ir en posiciones donde se espere un caracter o número.

```java
float pi1 = 3_.1415F; // Inválido
float pi2 = 3._1415F; // Inválido
long socialSecurityNumber1 = 999_99_9999_L; // Inválido
int x3 = 5_______2; // Válido
int x4 = 0_x52; // Inválido
int x5 = 0x_52; // Inválido
int x7 = 0x52_; // Inválido
int x8 = 13_112; // Válido
```
# [Collecciones](#collections)

Las colecciones son contenedores pertenecientes a la api collections de java.

## [Set](#set)

Es una interfaz que posee 3 implementaciones que poseen la característica de que sus elementos no se repitan.

### [HashSet](#hashset)

```java
Set<String> lista = new HashSet<>();

lista.add("Ignacio");
lista.add("José");
lista.add("Pedro");
lista.add("Ignacio"); // No se inserta
```

Si deseamos ingresar objetos personalizados deberemos sobreescribir los métodos `equals()` y `hashCode()`, puesto que si no, aunque se agreguen objetos con el mismo contenido, estas se agregaran al set de todas formas por ser instancias diferentes a nivel de memoria.

```java
public class Persona {

    int id;
    String nombre;

    public Persona(int id, String nombre) {
    	this.id = id;
        this.nombre = nombre;
    }

    @override
    public int hashCode() {
    	final int r = 19;
        return ;
    }

    @override
    public boolean equals(Persona p) {
    	return ...
    }
}
```

Ahora ya podremos agregar elementos de tipo `Persona` teniendo en cuenta que estos se diferenciarán a partir de los métodos sobreescritos.

```java
Set<Persona> hashSet = new HashSet<>();

hashSet.add(new Persona(1, "Ignacio"));
hashSet.add(new Persona(2, "Marcos"));
hashSet.add(new Persona(1, "Ignacio")); // No se agrega
```

### [TreeSet](#treeset)

Permite ingresar elementos únicos de forma ordenada de forma ascendente.

```java
Set<String> treeSet = new TreeSet();
treeSet.add("Ignacio");
treeSet.add("Andrea");
treeSet.add("Karla");
treeSet.add("Pedro");

treeSet.forEach(System.out::println);
// Andrea, Ignacio, Karla, Pedro
```

Si deseamos ingresar elementos de clases personalizadas es necesario implementar la interfaz [Comparable](sort-collections.md).

### [LinkedHashSet](#linkedhashset)

Permite ingresar elementos únicos ordenados de acuerdo al orden de agregación.

```java
Set<String> linkedHashSet = new LinkedHashSet();
linkedHashSet.add("Ignacio");
linkedHashSet.add("Andrea");
linkedHashSet.add("Karla");
linkedHashSet.add("Pedro");

linkedHashSet.forEach(System.out::println);
// Ignacio, Andrea, Karla, Pedro
```

Si deseamos ingresar elementos de clases personalizadas es necesario implementar la interfaz [Comparable](sort-collections.md).

## [Map](#map)

Si bien es cierto `Map` no pertenece a la api Collections se tomará en cuenta puesto que se utiliza como contenedor.

### [HashMap](#hashmap)

Permite ingresar elementos clave valor.
No permite valores duplicados en las claves y no se tiene en cuenta el orden.

```java
Map<String, String> hashMap = new HashMap<>();

hashMap.put("3", "Ignacio");
hashMap.put("5", "Antonio");
hashMap.put("3", null); // Sobreescribe el elemento con clave "3"
hashMap.put(null, "Jaime");
```

### [TreeMap](#treemap)

Permite ingresar elementos clave valor, de forma ordenada ascendentemente. Las claves no pueden ser `null`.

### [LinkedHashMap](#linkedhashmap)

Permite ingresar elementos clave valor, de forma ordenada en el orden de ingreso.

# [Stack](#stack)

Pila clásica LIFO.

```java
Stack<String> ila = new Stack<>();
```

Para ingresar elementos usamos `push()`:

```java
pila.push("Ignacio");
pila.push("José");
pila.push("Andrés");
```

Para remover los elementos usamos `pop()`:
```java
while(!pila.isEmpty()) {
	pila.pop(); // Elimina el último elemento ingresado
}
```

Si queremos saber que elemento fue el último en ingresar usamos `peek()`:

```java
pila.peek(); // "Andrés"
```

Podemos buscar un elemento usando `search()`:

```java
pila.search("José"); // 2
pila.search("Ignacio"); // 3
pila.search("Paloma"); // -1
```

Para iterar la pila podemos usar un foreach común:

```java
for(String el:pila) {
	System.out.println(el);
}
```

## Queue

### PriorityQueue

Permite ingresar elementos tomando en cuenta la prioridad.

Internamente es gestionado mediante un árbol binario, en el que la raíz sera la cabeza de la cola y siempre que se agreguen elementos se tendrá en cuenta la prioridad (quien sea el menor será el que tendrá más prioridad).


```java
Queue<String> cola = new PriorityQueue<>();
```

Para ingresar elementos a la cola usamos el método `offer()`:

```java
cola.offer("Ignacio");
cola.offer("Andrés");
cola.offer("María");
```

Para eliminar elementos usamos el método `poll()`:

```java
cola.poll();
```
# Ordenar Colecciones

Utilizando la api collection es posible ordenar fácilmente colecciones.

Usando el método sort es posible ordenar una lista:
```java
List<String> lista = new ArrayList<>();

lista.add("Ignacio");
lista.add("Ana");
lista.add("Carlos");

Collections.sort(lista);

System.out.println(lista);
```

## Interfaz Comparator

Si tenemos clases personalizadas tendremos que implementar la interfaz Comparator para poder definir quien es mayor o menor.

Si tenemos una clase (Persona):
```java
public class Persona {
	int id;
    String nombre;

    public Persona(int id, String nombre) {
    	this.id = id;
        this.nombre = nombre;
    }
    // Getters y Setters
}
```

Definimos una clase que implemente la interfaz Comparator y sobreescriva el método compare:
```java
import java.util.Comparator;
// Ordenamiento por nombre
public class NombreComparator implements Comparator<Persona> {
    @override
	public int compare(Persona obj1, Persona obj2) {
		return obj1.getNombre().compareTo(obj2.getNombre());
    }
}
```

Ya podremos ordenar por nombre:

```java
Collections.sort(lista, new NombreComparator());
System.out.println(lista);
```

También podremos definir una nueva implementación de la interfaz comparator de forma anónima:
```java
Collections.sort(lista, new Comparator<Persona>() {
    @override
	public int compare(Persona obj1, Persona obj2) {
		return obj1.getNombre().compareTo(obj2.getNombre());
    }
});
System.out.println(lista);
```

## Interfaz Comparable

Es posible implementar la interfaz `Comparable` en la clase en la que se vaya a necesitar comparar.

```java
public class Persona implements Comparable<Persona> {
	// Métodos y atributos

    @override
    public int compareTo(Persona p) {
    	return this.edad - p.edad;
    }
}
```

Y de la misma forma podremos utilizar `Collections.sort()`, solo que esta vez no habrá necesidad de implementar la interfaz `Comparator`.

```java
List<Persona> lista = new ArrayList<>();

lista.add(new Persona(/*...*/));
lista.add(new Persona(/*...*/));
lista.add(new Persona(/*...*/));

Collections.sort(lista);

System.out.println(lista);
```
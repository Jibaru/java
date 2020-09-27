# Singleton

Es un patrón de diseño que permite obtener tan sólo una única instancia de una clase.

## Estructura:

La estructura básica de una clase que implemente el patrón Singleton es la siguiente:

```java
public class Singleton {

    // La única instancia que se tendrá será
    // static y pertenecerá a la clase
    private static Singleton instancia;

    // Método Constructor privado
    private Singleton() {}

    // A traves de este método podremos acceder a la 
    // única instancia de la clase
    public static Singleton getInstance() {
        if(instancia == null) {
            instancia = new Singleton();
        }

        return instancia;
    }

}
```
## Ejemplo:

Podremos aplicar el patrón Singleton a una conexión de una base de datos.

```java
public class Conexion {

    private static Singleton instancia;

    private Conexion() {
        // Lógica de conexión
    }

    public static Conexion getInstance() {
        if(instancia == null) {
            instancia = new Conexion();
        }

        return instancia;
    }

}
```

También es posible aplicarla a alguna colección inalterable de datos.

```java
public class PaisDAO {

    private static PaisDAO instance;
    private List<String> paises;

    private PaisDAO() {
        paises = new ArrayList<>();

        paises.add(new Pais("PERÚ"));
        paises.add(new Pais("USA"));
        paises.add(new Pais("COLOMBIA"));
        paises.add(new Pais("MÉXICO"));
        paises.add(new Pais("CHILE"));
    }

    public static PaisDAO getInstance() {
        if(instance == null) {
            instance = new PaisDAO();
        }

        return instance;
    }

    public List<String> getPaises() {
        return paises;
    }

}

class Pais {

    private String nombre;

    public Pais(String nombre) {
        this.nombre = nombre;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    @override
    public String toString() {
        return "Pais(nombre=" + nombre + ")";
    }
}
```

Y para obtener la instancia de `PaisDAO` usamos el método `getInstance()`:

```java
PaisDAO paisDAO = PaisDAO.getInstance();

// Mostramos los datos de la lista de países de 
// la única instancia
paisDAO.getPaises().forEach(System.out::println);
// Pais(nombre=PERÚ)
// Pais(nombre=USA)
// Pais(nombre=COLOMBIA)
// Pais(nombre=MÉXICO)
// Pais(nombre=CHILE)
```
# [¿Cuándo usar clases anidadas y expresiones lambda?](#when-to-use-nested-local-anonymous-classes-and-lambda-expressions)

- <b>Clases locales: </b>Si necesitas crear más de una instancia de una clase, acceder a su constructor, o agregar uno nuevo.
- <b>Clases anónimas: </b>Si necesitas declarar más campos o métodos adicionales.
- <b>Expresiones lambda: </b>Si necesitas encapsular una acción que necesitas pasar a otro lugar; si quieres crear una instancia de una interfaz funcional y no es necesario ninguno de los criterior mencionados en los dos puntos anteriores.
- <b>Clases anidadas: </b>Si necesitas lo mismo que en una clase local, pero sin necesidad de querer acceder a variables locales o parámetros de un métodos.
  - Use una `clase interna` si es necesario acceder a miembros de instancia `no-public` y métodos.
  - Use una `clase anidada static` si no lo necesita.
<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Composición". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación y Excepciones.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# Tema 4.1. Composición

***

# ✅ **1. Composición en C con `struct`: puntos y línea**

### Respuesta

En C, la composición se logra definiendo `struct` que contienen otros `struct` como campos internos. Esto permite construir entidades más complejas a partir de otras más simples. En el caso de una línea formada por dos puntos, la estructura `Linea` contendrá dos variables de tipo `Punto`, ilustrando la típica relación “tiene‑un”. Esto sigue siendo programación estructurada, ya que no existe ocultación de información ni comportamientos asociados a las estructuras por defecto.

Las funciones externas permiten operar sobre estas estructuras simulando métodos, aunque sin la seguridad que aporta la encapsulación orientada a objetos. Calcular distancias o longitudes es simplemente una operación matemática que usa los campos públicos de las estructuras. Se observa que la responsabilidad de la integridad de los datos recae completamente en el programador, ya que no existen restricciones que impidan modificar libremente los valores internos.

```c
#include <math.h>

typedef struct {
    double x;
    double y;
} Punto;

typedef struct {
    Punto a;
    Punto b;
} Linea;

double distancia(Punto p1, Punto p2) {
    double dx = p1.x - p2.x;
    double dy = p1.y - p2.y;
    return sqrt(dx*dx + dy*dy);
}

double longitud(Linea l) {
    return distancia(l.a, l.b);
}
```

***

# ✅ **2. Transformación a orientación a objetos en Java**

### Respuesta

En Java, el mismo ejemplo se expresa mediante clases, lo que permite encapsular los datos y asociar comportamientos a los objetos. Mediante atributos privados y ausencia de setters, se garantiza que los puntos sean inmutables. La composición aparece porque una `Linea` contiene dos objetos `Punto`, también inmutables, creando una estructura que no puede modificarse una vez construida. Esto proporciona más seguridad que la versión en C.

La ocultación de información impide modificar las coordenadas externas al objeto, lo que fortalece la integridad del estado interno. Además, los métodos dentro de cada clase proporcionan operaciones relacionadas directamente con ellas, como el cálculo de distancia entre puntos o la longitud de una línea. Esto muestra cómo la POO, mediante la composición, organiza mejor el código y protege los datos internos.

```java
final class Punto {
    private final double x, y;

    public Punto(double x, double y) {
        this.x = x; this.y = y;
    }

    public double distancia(Punto otro) {
        double dx = x - otro.x;
        double dy = y - otro.y;
        return Math.sqrt(dx*dx + dy*dy);
    }
}

final class Linea {
    private final Punto a, b;

    public Linea(Punto a, Punto b) {
        this.a = a; this.b = b;
    }

    public double longitud() {
        return a.distancia(b);
    }
}
```

***

# ✅ **3. Multiplicidad en la composición**

### Respuesta

La multiplicidad expresa cuántas instancias de una clase están asociadas a otra dentro de una relación estructural. En composición, esta relación suele ser más fuerte porque los objetos contenidos forman parte del ciclo de vida del contenedor. En modelos UML, estas multiplicidades permiten entender la estructura interna del sistema, así como las restricciones del número de objetos que puede contener una entidad.

En el ejemplo de `Linea` y `Punto`, una línea contiene exactamente dos puntos, lo que se expresa como multiplicidad **2** desde `Linea` hacia `Punto`. En sentido inverso, un `Punto` concreto no pertenece necesariamente a ninguna línea o podría formar parte de varias, dependiendo del diseño. Asumiendo el caso habitual, la multiplicidad sería **0..**\* desde `Punto` hacia `Linea`.

***

# ✅ **4. Composición fuerte vs. composición débil**

### Respuesta

La composición fuerte implica que los objetos contenidos dependen completamente del contenedor y no existen de manera independiente. En esta relación, la destrucción del objeto contenedor implica la destrucción de todos sus componentes. Esta relación es propia de la composición estricta en UML, donde los componentes no pueden ser compartidos entre múltiples contenedores.

En cambio, la composición débil suele llamarse agregación o asociación agregada. En ella, los objetos pueden existir de manera independiente y pueden pertenecer a varios contenedores simultáneamente. El ciclo de vida no está ligado y la destrucción del contenedor no afecta a los objetos que contiene. Esta forma es más flexible y habitual en sistemas con recursos compartidos.

***

# ✅ **5. Uso de otras clases como parámetros: ¿composición o dependencia?**

### Respuesta

Cuando una clase utiliza otra únicamente como parámetro o valor de retorno en un método, o la crea de manera local dentro de un método, no se considera composición. La composición implica que el objeto que contiene mantiene una relación estructural y de pertenencia con el contenido, lo que no ocurre en estos casos. Las variables locales o parámetros son temporales y no forman parte del estado interno del objeto.

Estas situaciones se clasifican como dependencias, ya que la clase depende de otra para realizar alguna operación, pero no mantiene una relación estable con ella. La dependencia es una relación mucho más débil y temporal que la composición o agregación. En UML suele representarse con una flecha discontinua.

***

# ✅ **6. Composición fuerte y débil con `Linea` y `Punto`**

### Respuesta

En una composición fuerte entre `Linea` y `Punto`, los puntos se crean dentro de la línea y no se exponen hacia el exterior. El usuario no tiene acceso directo a ellos y no se permite que existan fuera de la línea. Esto asegura que el ciclo de vida de los puntos depende completamente del de la línea y que el diseño refleja una estructura rígida pero segura.

```java
// Composición fuerte
final class LineaFuerte {
    private final Punto a = new Punto(0,0);
    private final Punto b = new Punto(1,1);

    public double longitud() { return a.distancia(b); }
}
```

En la composición débil, los puntos vienen desde fuera y pueden existir independientemente de la línea. La línea no controla su ciclo de vida, sólo mantiene referencias. Este modelo permite reutilizar puntos entre distintas líneas.

```java
// Composición débil
final class LineaDebil {
    private final Punto a, b;

    public LineaDebil(Punto a, Punto b) {
        this.a = a; this.b = b;
    }

    public double longitud() { return a.distancia(b); }
}
```

***

# ✅ **7. Destrucción en composición fuerte en Java**

### Respuesta

En Java, la destrucción de objetos no está controlada explícitamente por el programador. Incluso en una composición fuerte, no se llama a ningún método que destruya los objetos internos. Esto se debe a que Java utiliza un recolector automático de basura que libera memoria cuando ya no existen referencias a un objeto. Así, el ciclo de vida está gestionado por la máquina virtual y no por el código del programador.

Por ello, aunque conceptualmente la línea “destruye” los puntos cuando desaparece, en realidad simplemente deja de existir una referencia a ellos, y el recolector los elimina automáticamente. Esta abstracción simplifica la gestión de memoria y reduce errores como fugas o dobles liberaciones, comunes en lenguajes como C.

***

# ✅ **8. Ejemplo de composición débil con departamento y profesores (arrays)**

### Respuesta

En esta composición débil, el departamento mantiene una colección de profesores, representada mediante un array interno que no se expone directamente. Los profesores existen independientemente del departamento y se pueden añadir o eliminar. La lista tiene un límite de 50 elementos y ofrece métodos controlados para acceder a ellos sin romper la encapsulación. Esto evita que se modifique accidentalmente el array interno desde fuera.

Además, existe un director, que también es un profesor del departamento y cuya presencia está garantizada desde la construcción del objeto. La invariante exige que el director siempre pertenezca al conjunto de profesores, por lo que cualquier operación que elimine profesores o cambie el director debe verificar esta condición y lanzar excepciones cuando no se cumpla. Esta lógica asegura la consistencia interna del objeto ante cambios.

```java
final class Profesor {
    private final String nombre;
    public Profesor(String nombre){ this.nombre = nombre; }
    public String getNombre() { return nombre; }
}

final class Departamento {
    private final Profesor[] profesores = new Profesor[50];
    private int num = 0;
    private Profesor director;

    public Departamento(Profesor directorInicial) {
        profesores[0] = directorInicial;
        num = 1;
        director = directorInicial;
    }

    public void addProfesor(Profesor p) {
        if (num >= 50) throw new IllegalStateException("Lleno");
        profesores[num++] = p;
    }

    public void removeProfesor(int pos) {
        if (pos < 0 || pos >= num) throw new IllegalArgumentException();
        if (profesores[pos] == director)
            throw new IllegalStateException("No se puede eliminar al director");
        for (int i = pos; i < num - 1; i++)
            profesores[i] = profesores[i+1];
        num--;
    }

    public int getNumProfesores() { return num; }

    public Profesor getProfesor(int pos) {
        if (pos < 0 || pos >= num) throw new IllegalArgumentException();
        return profesores[pos];
    }

    public void setDirector(Profesor p) {
        boolean encontrado = false;
        for (int i = 0; i < num; i++)
            if (profesores[i] == p) encontrado = true;
        if (!encontrado)
            throw new IllegalArgumentException("El director debe estar en el departamento");
        director = p;
    }
}
```

***

# ✅ **9. Versión con `List` y discusión del acceso**

### Respuesta

El uso de `List` simplifica notablemente la implementación porque evita gestionar manualmente la capacidad, los desplazamientos internos o el control del tamaño. Esto elimina gran parte del código que antes manipulaba índices y posiciones. Las operaciones de añadir y eliminar elementos se vuelven más legibles, y se reduce el riesgo de errores relacionados con índices fuera de rango.

Sin embargo, si se devolviera directamente la lista interna de profesores, el usuario podría modificarla desde fuera, comprometiendo completamente la encapsulación y el control de invariantes. Para evitarlo, se devolvería una copia superficial mediante `new ArrayList<>(lista)` o una vista inmodificable con `Collections.unmodifiableList(lista)`. De este modo, se protege la estructura interna del objeto.

```java
final class Departamento {
    private final List<Profesor> profesores = new ArrayList<>();
    private Profesor director;

    public Departamento(Profesor d) {
        profesores.add(d);
        director = d;
    }

    public void addProfesor(Profesor p) { profesores.add(p); }

    public void removeProfesor(int pos) {
        Profesor p = profesores.get(pos);
        if (p == director)
            throw new IllegalStateException("No se puede eliminar al director");
        profesores.remove(pos);
    }

    public int getNumProfesores() { return profesores.size(); }

    public Profesor getProfesor(int pos) {
        return profesores.get(pos);
    }

    public List<Profesor> getProfesoresSeguro() {
        return List.copyOf(profesores);
    }

    public void setDirector(Profesor p) {
        if (!profesores.contains(p))
            throw new IllegalArgumentException();
        director = p;
    }
}
```

***

# ✅ **10. Composición recursiva: Persona con madre**

### Respuesta

La composición recursiva aparece cuando una clase contiene un atributo del mismo tipo. Un caso típico es un árbol genealógico donde una persona tiene una madre, que es otra persona. Para evitar ciclos infinitos y mantener la consistencia, el objeto suele ser inmutable, lo que asegura que las relaciones no puedan alterarse una vez establecidas. Esto es habitual en estructuras como árboles o listas encadenadas.

Este patrón permite modelar jerarquías naturales, genealogías y estructuras recursivas como nodos de árboles, carpetas dentro de carpetas o listas enlazadas. La recursividad aporta flexibilidad para representar estructuras complejas sin necesidad de conocer su tamaño de antemano. Un ejemplo ilustrativo en Java sería:

```java
final class Persona {
    private final String nombre;
    private final Persona madre;

    public Persona(String nombre, Persona madre) {
        this.nombre = nombre;
        this.madre = madre;
    }

    public String getNombre() { return nombre; }
    public Persona getMadre() { return madre; }

    public String cadenaMaterna() {
        if (madre == null) return nombre;
        return nombre + " -> " + madre.cadenaMaterna();
    }

    public static void main(String[] args) {
        Persona abuela = new Persona("Abuela", null);
        Persona madre = new Persona("Madre", abuela);
        Persona hijo  = new Persona("Hijo", madre);

        System.out.println(hijo.cadenaMaterna());
    }
}
```

Otros ejemplos clásicos incluyen nodos de un árbol binario, elementos de una lista enlazada o directorios del sistema de archivos.

***

# ✅ **11. Composición bidireccional**

### Respuesta

Una composición bidireccional implica que los objetos se conocen mutuamente: el contenedor mantiene referencias a los componentes, y a su vez cada componente mantiene una referencia al contenedor. Esto permite navegar la relación en ambos sentidos, lo que puede ser útil para ciertos algoritmos o invariantes. Sin embargo, requiere cuidado para evitar inconsistencias al modificar la relación.

En el caso de `Profesor` y `Departamento`, cada profesor debería tener un atributo que indique a qué departamento pertenece. De este modo, cuando se añade un profesor al departamento, también debe actualizarse el campo correspondiente en el profesor. Y, del mismo modo, al eliminarlo, se eliminaría la referencia inversa. Esto exige implementar métodos de enlace y desenlace que mantengan la coherencia de la relación bidireccional.

***


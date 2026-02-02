<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Clases y Objetos". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: ninguno.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 1. Clases y objetos

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

### Las cuatro características fundamentales de la Programación Orientada a Objetos son **encapsulamiento**, **abstracción**, **herencia** y **polimorfismo**. El encapsulamiento consiste en proteger los datos internos de un objeto, permitiendo que solo se acceda a ellos mediante métodos controlados. Esto evita modificaciones incorrectas y organiza mejor el código. La abstracción, por su parte, permite centrarse únicamente en los aspectos esenciales de un objeto, ocultando detalles internos y facilitando que otros usen una clase sin necesidad de conocer su implementación exacta.

## La herencia permite crear nuevas clases basadas en otras ya existentes, heredando comportamiento y atributos. Gracias a ello se reutiliza código y se construyen jerarquías lógicas que hacen más sencillo mantener y ampliar programas. Finalmente, el polimorfismo posibilita que la misma operación produzca comportamientos distintos según el tipo de objeto que la ejecute. Este mecanismo proporciona flexibilidad, ya que permite escribir código general que funciona con diferentes tipos derivados sin necesidad de modificarse.

## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Existen numerosos lenguajes que permiten trabajar con programación orientada a objetos, pero algunos han adquirido especial relevancia por su amplio uso y soporte. Uno de los más representativos es **Java**, un lenguaje diseñado específicamente con la POO como eje central y ampliamente utilizado en desarrollo empresarial, aplicaciones Android y sistemas de gran escala. De manera similar, **C++** es otro lenguaje muy popular que, aunque originalmente derivado de C, incorporó mecanismos de orientación a objetos y ha mantenido su importancia en entornos donde se requiere alto rendimiento.

### También destaca **Python**, que ofrece un enfoque flexible y sencillo de la POO, permitiendo definir clases y objetos de forma muy accesible para principiantes. Finalmente, **C#** es otro lenguaje orientado a objetos ampliamente usado, especialmente en el ecosistema de Microsoft y en el desarrollo de videojuegos con motores como Unity. Todos estos lenguajes no solo permiten aplicar los principios de la programación orientada a objetos, sino que también muestran cómo la POO se ha convertido en un enfoque fundamental dentro del desarrollo moderno.

## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### Antes de la aparición de la Programación Orientada a Objetos, uno de los paradigmas predominantes fue la **programación estructurada**. Este enfoque se basa en dividir un programa en bloques lógicos y emplear estructuras de control claras, como secuencias, condicionales y bucles. Su objetivo es evitar el uso excesivo de instrucciones como `goto`, que dificultan seguir el flujo del programa. Gracias a esta disciplina, el código resulta más legible y predecible, y facilita comprender qué ocurre en cada parte del programa. Lenguajes como C representan muy bien este paradigma, ya que promueven un estilo de programación lineal y ordenado.

### Un paso más allá dentro de los paradigmas previos a la POO es la **programación modular**, que surge para mejorar la organización del código a gran escala. En este enfoque, el programa se divide en módulos independientes, cada uno encargado de una responsabilidad concreta. Estos módulos pueden compilarse y desarrollarse por separado, facilitando la colaboración entre múltiples desarrolladores y evitando mezclar funciones que no están relacionadas. En C, esto se aprecia claramente mediante el uso de ficheros `.c` y `.h`, donde cada módulo contiene su implementación y su interfaz pública. La programación modular introduce así un nivel de organización superior a la estructurada, y constituye una de las bases conceptuales sobre las que luego se construiría la POO.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### En programación orientada a objetos, un objeto se define fundamentalmente por **atributos**, **métodos** y **estado**. Los **atributos** representan los datos que describen al objeto, es decir, sus características. En Java suelen ser variables internas de la clase, como por ejemplo el tamaño, el color o cualquier información relevante. Estos atributos permiten diferenciar un objeto de otro incluso cuando pertenecen a la misma clase, de manera similar a cómo una estructura en C contiene diferentes campos de datos.

### Los **métodos** representan las acciones que el objeto puede realizar o las operaciones que pueden ejecutarse sobre él. Son equivalentes conceptuales a las funciones en C, pero asociadas directamente con un tipo de dato complejo (la clase). Gracias a los métodos, un objeto no solo almacena información, sino que también sabe cómo manipularla o cómo interactuar con otros objetos del programa.

### Finalmente, el **estado** de un objeto se refiere a los valores concretos que tienen sus atributos en un momento determinado. Aunque dos objetos pertenezcan a la misma clase y dispongan de los mismos atributos y métodos, su estado puede ser distinto porque los datos almacenados pueden variar. Este concepto resulta esencial en POO, ya que el comportamiento de un objeto puede depender directamente del estado en el que se encuentre, lo que permite modelar situaciones reales de una manera más natural.

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### En programación orientada a objetos, una **clase** se entiende como un modelo o plantilla que describe qué atributos y métodos tendrán los objetos creados a partir de ella. No representa algo concreto del programa, sino un concepto general. Por ejemplo, una clase `Coche` puede definir que todos los coches tienen un color, una velocidad y ciertos comportamientos como acelerar o frenar. Sin embargo, por sí misma, la clase no es un coche real dentro del programa.

### Un **objeto**, en cambio, es una entidad concreta creada a partir de una clase. Es posible decir que el objeto es la “materialización” de la clase. Siguiendo el ejemplo, un objeto podría ser un coche específico, como uno rojo que va a 60 km/h. Por tanto, **una clase no es lo mismo que un objeto**, aunque estén íntimamente relacionados: la clase define, el objeto existe y actúa. A este proceso de crear un objeto a partir de una clase se le llama **instanciar**, y al objeto resultante se le denomina **instancia**.

### No todos los lenguajes orientados a objetos manejan necesariamente el concepto de clase. La mayoría sí lo utilizan, como Java, C#, Python o C++. Sin embargo, existen lenguajes orientados a objetos que no funcionan estrictamente con clases, sino con **prototipos**, como JavaScript. En estos lenguajes, los objetos se derivan directamente de otros objetos sin necesidad de definir una clase formal. Esto demuestra que la POO puede implementarse de diferentes formas según el diseño del lenguaje.

## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### En la mayoría de lenguajes orientados a objetos, los objetos suelen almacenarse en una zona de memoria llamada **heap**. Esta área se utiliza para asignaciones dinámicas, es decir, aquellas que se realizan durante la ejecución del programa. Cuando en Java se crea un objeto con `new`, ese objeto se guarda en el heap, mientras que la variable que lo referencia suele almacenarse en la pila (*stack*). Este funcionamiento es similar al uso de `malloc` en C, pero con un sistema mucho más seguro y automatizado, lo que evita muchos errores comunes relacionados con memoria.

### No obstante, el lugar exacto donde se almacenan los objetos **no es igual en todos los lenguajes**. En C++, por ejemplo, un objeto puede almacenarse en la pila o en el heap dependiendo de cómo se cree: un objeto creado directamente sin `new` se almacena en la pila, mientras que un objeto creado con `new` se almacena en el heap. En lenguajes como Python o JavaScript, prácticamente todos los objetos residen en el heap, ya que la gestión de memoria está completamente abstraída del programador. Por tanto, la ubicación en memoria depende del lenguaje y del modelo de ejecución que este utilice.

### La **recolección de basura** (*garbage collection*) es un mecanismo automático utilizado por lenguajes como Java o Python para liberar memoria que ya no está siendo utilizada por el programa. Este sistema detecta cuándo un objeto deja de ser accesible —porque ninguna referencia apunta a él— y libera su espacio en el heap sin intervención del programador. Gracias a este proceso, se reducen errores frecuentes en C/C++ como fugas de memoria (*memory leaks*) o intentos de liberar memoria dos veces. Aunque añade cierta carga al rendimiento, el *garbage collector* permite escribir programas más seguros y fáciles de mantener.

## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### En programación orientada a objetos, un **método** es una función asociada a una clase y, por tanto, a los objetos que se crean a partir de ella. Mientras que en C se definen funciones independientes, en Java los métodos forman parte del comportamiento de un objeto y pueden acceder a sus atributos internos. Esto permite que cada objeto “sepa” cómo realizar determinadas acciones, como calcular un valor, modificar datos o interactuar con otros objetos del programa.

### La **sobrecarga de métodos** (*method overloading*) consiste en definir varios métodos con el mismo nombre dentro de una misma clase, pero con diferentes listas de parámetros. Esto significa que un método puede tener varias versiones, cada una adaptada a distintos tipos o cantidades de datos de entrada. El compilador decide automáticamente cuál debe ejecutarse según los argumentos utilizados en la llamada. Esta característica proporciona flexibilidad al programador, ya que permite ofrecer distintas alternativas de uso sin necesidad de inventar nombres diferentes para cada variante.

### Este mecanismo no debe confundirse con la sobrescritura de métodos, que ocurre en herencia. La sobrecarga se produce dentro de la misma clase y se resuelve en tiempo de compilación, mientras que la sobrescritura implica redefinir un método heredado y se decide en tiempo de ejecución. En conjunto, los métodos y su sobrecarga permiten construir clases más expresivas, claras y fáciles de usar.


## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### Se propone una clase mínima llamada `Punto` con dos atributos `x` e `y` con **visibilidad por defecto** (sin `public`, `private` ni `protected`). Se incluye un método `calculaDistanciaAOrigen()` que retorna la distancia euclídea al origen `(0,0)`, usando la fórmula √(x² + y²). Al ser un ejemplo básico, no se añaden constructores ni validaciones; el objetivo es ilustrar la estructura de una clase y el uso de un método de instancia.

### Para mostrar su uso, se crea una instancia, se asignan valores a `x` e `y` y se invoca el método para obtener la distancia, imprimiendo el resultado por consola. En Java, `Math.sqrt` calcula la raíz cuadrada y `Math.pow` no es necesario aquí; con `x * x` y `y * y` es suficiente y eficiente. El ejemplo es auto-contenido y puede compilarse sin paquetes para simplificar.

```java
// Clase mínima Punto.java
class Punto {
    // Visibilidad por defecto (package-private)
    double x;
    double y;

    // Método que calcula la distancia al origen (0,0)
    double calculaDistanciaAOrigen() {
        return Math.sqrt((x * x) + (y * y));
    }
}
```

```java
// Ejemplo de uso: Main.java
public class Main {
    public static void main(String[] args) {
        Punto p = new Punto();
        p.x = 3.0;
        p.y = 4.0;

        double distancia = p.calculaDistanciaAOrigen();
        System.out.println("Distancia al origen: " + distancia); // Debería imprimir 5.0
    }
}
```


## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### En un programa Java, el **punto de entrada** es siempre el método `main`, definido con la firma `public static void main(String[] args)`. Este método es el que la máquina virtual de Java ejecuta en primer lugar cuando arranca el programa. A diferencia de C, donde `main` pertenece a un archivo fuente, en Java este método debe estar dentro de una clase, ya que todo el código debe formar parte de alguna clase. Sin este método, el programa no puede iniciarse de forma autónoma, incluso aunque existan otras clases y métodos correctamente definidos.

### La palabra clave **`static`** indica que un método o atributo pertenece a la **clase**, y no a una instancia concreta. Esto significa que puede utilizarse sin necesidad de crear un objeto. En el caso del `main`, es obligatorio que sea estático porque al iniciarse el programa aún no existe ninguna instancia creada desde la cual poder llamar a ese método. Sin embargo, `static` **no se usa exclusivamente** en el método `main`; también se emplea para atributos compartidos entre todos los objetos de una clase o para métodos que no dependen del estado individual de una instancia, como funciones utilitarias.

### La combinación **`static final`** se utiliza para definir **constantes**, es decir, valores que pertenecen a la clase y que no pueden modificarse después de ser asignados. En Java, esto es la forma habitual de declarar constantes similares a las de C (`#define` o `const`). Por ejemplo, `static final double PI = 3.14159;` permite que el valor esté disponible para todas las instancias, sea único y permanezca inmutable. Esta combinación favorece la claridad del código y evita errores relacionados con la modificación accidental de valores que deberían ser fijos.

***

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Para compilar un programa Java desde la línea de comandos, se utiliza el comando `javac` seguido del nombre del archivo `.java`. Esto genera uno o varios ficheros `.class` que contienen el *bytecode*. Posteriormente, se ejecuta el programa mediante el comando `java`, indicando el nombre de la clase que contiene el método `main` (sin la extensión). Por ejemplo, si se tiene `Main.java`, la secuencia sería `javac Main.java` para compilar y `java Main` para ejecutarlo. Este proceso recuerda a la compilación en C, pero en Java se generan ficheros intermedios interpretados por la máquina virtual antes de ejecutarse.

### Java se considera un lenguaje **compilado e interpretado al mismo tiempo**. Primero se compila a un formato intermedio (*bytecode*) mediante `javac`, y después este *bytecode* es interpretado o ejecutado por la **Máquina Virtual de Java (JVM)**. La JVM es un entorno de ejecución que actúa como una capa independiente del sistema operativo, lo que permite que un mismo programa funcione igual en Windows, Linux o macOS sin necesidad de recompilarlo. Así se consigue la filosofía de Java: *write once, run anywhere*.

### El **bytecode** es un conjunto de instrucciones de bajo nivel que no dependen de ningún sistema operativo o procesador concreto. Este bytecode se almacena en los archivos `.class` generados por el compilador. La JVM se encarga de interpretar o convertir estas instrucciones en operaciones reales para la máquina física. Gracias a este modelo, Java logra portabilidad, seguridad y un control eficiente de la ejecución, aunque con un pequeño coste en rendimiento respecto a la compilación directa a código máquina, como ocurre en C o C++.

## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### En Java, la palabra clave **`new`** se utiliza para **crear objetos** en memoria dinámica (heap) e **invocar su constructor**. Al usarse, se reserva el espacio necesario para los atributos del objeto y se devuelve una **referencia** a esa región de memoria. En el ejemplo de la clase `Punto`, la expresión `new Punto()` crea un nuevo `Punto` e inicializa su estado según defina el constructor de la clase (explícito o el **constructor por defecto** si no se declaró ninguno).

### Un **constructor** es un método especial cuyo propósito es **inicializar** un objeto cuando se crea. Se llama automáticamente al usar `new`, **no tiene tipo de retorno** (ni siquiera `void`) y su **nombre es exactamente el de la clase**. Puede estar **sobrecargado** para permitir varias formas de inicialización (por ejemplo, con o sin parámetros). Si no se define ninguno, Java proporciona un **constructor por defecto** sin parámetros que no realiza más que la inicialización por defecto de los campos (cero para números, `false` para booleanos y `null` para referencias).

### A continuación, se muestra un ejemplo de clase `Empleado` con **tres campos** (`dni`, `nombre`, `apellidos`) y un **constructor con parámetros** que obliga a crear la instancia en un estado válido desde el primer momento. También se incluye, a modo ilustrativo, un **constructor por defecto**:

```java
public class Empleado {
    String dni;
    String nombre;
    String apellidos;

    // Constructor por defecto (opcional)
    public Empleado() {
        // Inicializaciones por defecto si se desea
        this.dni = "";
        this.nombre = "";
        this.apellidos = "";
    }

    // Constructor con parámetros
    public Empleado(String dni, String nombre, String apellidos) {
        this.dni = dni;
        this.nombre = nombre;
        this.apellidos = apellidos;
    }

    // Ejemplo de uso
    public static void main(String[] args) {
        Empleado e1 = new Empleado("12345678A", "Ana", "García Pérez");
        Empleado e2 = new Empleado(); // usa el constructor por defecto
        System.out.println(e1.nombre + " " + e1.apellidos + " (" + e1.dni + ")");
    }
}
```


## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### La referencia **`this`** en Java señala explícitamente a la **instancia actual** del objeto dentro de sus métodos o constructores. Se utiliza para acceder a los atributos y métodos del propio objeto, y es especialmente útil cuando hay **sombras de nombres** (por ejemplo, parámetros de un constructor con el mismo nombre que los atributos). También permite **encadenar constructores** dentro de la misma clase usando `this(...)`, así como pasar la referencia del propio objeto a otros métodos.

### No todos los lenguajes usan el mismo nombre para esta referencia. En **Java, C#, Kotlin** se emplea `this`; en **C++** existe el puntero `this` (accedido como `this->`); en **Python** no es una palabra reservada, pero por convención se pasa el parámetro `self` al definir métodos; en **JavaScript** también existe `this`, aunque su semántica depende del contexto de llamada (con `bind`, `call`, funciones flecha, etc.). Por tanto, el concepto es común en POO, pero el **nombre y el comportamiento** pueden variar según el lenguaje.

### En la clase `Punto`, `this` puede usarse para **distinguir atributos** de los parámetros en un constructor y para **invocar métodos** del propio objeto. A continuación, un ejemplo mínimo que también incluye el método `calculaDistanciaAOrigen`:

```java
class Punto {
    double x; // visibilidad por defecto (package-private)
    double y;

    // Constructor con parámetros que usan los mismos nombres que los atributos
    Punto(double x, double y) {
        this.x = x; // 'this.x' se refiere al atributo; 'x' al parámetro
        this.y = y;
    }

    // Método de instancia que usa 'this' de forma explícita (opcional)
    double calculaDistanciaAOrigen() {
        double dx = this.x; // 'this' aquí es redundante pero ilustrativo
        double dy = this.y;
        return Math.sqrt(dx * dx + dy * dy);
    }

    // Ejemplo de método que encadena otro constructor de la misma clase
    Punto() {
        this(0.0, 0.0); // llama al otro constructor
    }
}
```


## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Para calcular la distancia entre el objeto actual (`this`) y otro punto recibido como parámetro, se puede implementar un método `distanciaA(Punto otro)`. La distancia euclídea en 2D se obtiene aplicando la fórmula √((x₂ − x₁)² + (y₂ − y₁)²). En este contexto, `this.x` y `this.y` representan las coordenadas del punto actual, mientras que `otro.x` y `otro.y` representan las del punto pasado como argumento. Es suficiente con restar componentes, elevar al cuadrado cada diferencia, sumarlas y aplicar `Math.sqrt`.

### Conviene validar que el parámetro no sea `null` si se quiere robustez adicional, ya que llamar al método con `null` produciría un `NullPointerException` al intentar acceder a `otro.x` o `otro.y`. En un ejemplo mínimo, puede omitirse esa validación para centrarse en la mecánica del cálculo; no obstante, en código de producción se recomienda comprobar el argumento y lanzar una excepción clara si no es válido.

```java
class Punto {
    double x; // visibilidad por defecto (package-private)
    double y;

    Punto() {
        this(0.0, 0.0);
    }

    Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    double calculaDistanciaAOrigen() {
        return Math.sqrt((this.x * this.x) + (this.y * this.y));
    }

    // Nuevo método: distancia entre 'this' y el punto 'otro'
    double distanciaA(Punto otro) {
        // Opcional: validar null
        // if (otro == null) throw new IllegalArgumentException("El punto no puede ser null");

        double dx = otro.x - this.x;
        double dy = otro.y - this.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}

// Ejemplo de uso
class Main {
    public static void main(String[] args) {
        Punto p1 = new Punto(1.0, 2.0);
        Punto p2 = new Punto(4.0, 6.0);
        double d = p1.distanciaA(p2); // distancia entre p1 y p2
        System.out.println("Distancia p1->p2 = " + d); // Debería imprimir 5.0
    }
}
```

### Si se desea mayor precisión numérica en cálculos muy grandes o muy pequeños, puede emplearse `double` como aquí o considerar `BigDecimal` para escenarios financieros (aunque no es usual en geometría básica).



## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### En Java, cuando se pasa un objeto como parámetro —por ejemplo, un `Punto`— se pasa **la referencia por valor**. Esto significa que el método recibe **una copia de la referencia**, pero ambas referencias apuntan al **mismo objeto** en memoria. Por tanto, si dentro del método se modifica algún atributo del objeto recibido, esos cambios **sí afectan** al objeto original fuera del método. Lo que no puede modificarse es la referencia en sí de forma que el objeto externo cambie de identidad, ya que la referencia se copia, pero el contenido del objeto sí es modificable.

### Sin embargo, cuando se pasa un tipo primitivo como `int`, `double`, `boolean`, etc., se pasa **por copia del valor**. Esto implica que el método recibe una variable independiente con el mismo valor, pero totalmente separada de la original. Si dentro del método se cambia ese entero, el cambio **no afecta** al valor externo. Esto es equivalente al paso por valor típico que se usa en C, donde los tipos primitivos se copian y son independientes del original.

### Esta diferencia provoca que el comportamiento sea distinto entre objetos y tipos primitivos: los objetos permiten modificar su estado desde dentro del método —porque se comparte la misma instancia— mientras que los primitivos no, porque sólo se copia el valor. Es importante comprender esta distinción para evitar errores al trabajar con estructuras complejas y para entender mejor cómo Java gestiona la memoria y las referencias.

## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### En Java, **`toString()`** es un método heredado de la clase base `Object` que devuelve una **representación textual** del objeto. Se utiliza automáticamente cuando se concatena el objeto con cadenas (por ejemplo, en `System.out.println(obj)`) o cuando una API espera texto y recibe un objeto. Por defecto, `toString()` muestra el nombre de la clase y un identificador basado en el *hash code*, por lo que suele **sobrescribirse** para ofrecer una representación legible y útil del estado del objeto (por ejemplo, mostrando sus campos principales).

### Este concepto existe en otros lenguajes, aunque con nombres o convenciones distintas. En **C#** también se llama `ToString()` y cumple un papel equivalente. En **Python**, el método comparable es `__str__` (y `__repr__` para una representación más técnica). En **JavaScript**, todos los objetos tienen `toString()`, si bien su comportamiento puede variar según el prototipo. En **C++**, no hay un método estándar universal, pero se emula el comportamiento sobrecargando el operador de inserción en flujo (`operator<<`) para imprimir objetos.

```java
// Ejemplo: sobrescritura de toString() en la clase Punto
class Punto {
    double x; // visibilidad por defecto (package-private)
    double y;

    Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    double calculaDistanciaAOrigen() {
        return Math.sqrt((x * x) + (y * y));
    }

    double distanciaA(Punto otro) {
        double dx = otro.x - this.x;
        double dy = otro.y - this.y;
        return Math.sqrt(dx * dx + dy * dy);
    }

    @Override
    public String toString() {
        // Representación legible y compacta
        return "Punto(x=" + x + ", y=" + y + ")";
    }
}

// Ejemplo de uso
class Main {
    public static void main(String[] args) {
        Punto p = new Punto(3.0, 4.0);
        System.out.println(p); // Invoca implícitamente p.toString() -> "Punto(x=3.0, y=4.0)"
    }
}
```

### Si se desea una versión más “técnica” o útil para depuración, puede incluirse también el *hash code* o formatos JSON; lo importante es que `toString()` ayude a **entender rápidamente el estado** del objeto al imprimirlo.



## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


### En C, un `struct` permite agrupar datos bajo un mismo tipo, lo que puede recordar superficialmente a una clase en programación orientada a objetos. Ambos mecanismos permiten definir un tipo compuesto formado por varios campos, y ambos posibilitan crear variables —o instancias— de ese tipo. Sin embargo, esta similitud es únicamente estructural; un `struct` solo describe datos, mientras que una clase describe **datos + comportamiento**. Es decir, un `struct` es un contenedor pasivo, mientras que una clase representa un concepto activo cuyas instancias pueden “hacer cosas” mediante métodos.

### Para que un `struct` en C se pareciera realmente a una clase, le faltarían varios elementos esenciales. En primer lugar, necesitaría **métodos asociados**, de modo que el propio tipo supiera ejecutar operaciones sobre sus datos, cosa que en C debe hacerse por funciones externas. También carece de **encapsulamiento**, ya que todos los campos del `struct` son siempre públicos y accesibles directamente. Además, un `struct` no tiene **constructores**, **destructores**, **herencia**, **polimorfismo**, ni ningún mecanismo que permita vincular datos y comportamiento de forma automática o segura.

### Finalmente, aunque en C es posible imitar algunos aspectos de la programación orientada a objetos mediante punteros a funciones o estructuras más complejas, el lenguaje no ofrece soporte nativo para conceptos como métodos de instancia, sobrecarga, visibilidad, o referencias a `this`. Por eso, aunque un `struct` puede considerarse un precursor conceptual de la clase, no puede funcionar como una verdadera clase sin añadir manualmente gran parte de la lógica que en lenguajes como Java está integrada de forma natural.


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### Para “emular” una clase `Punto` en C, se puede definir un `struct` que agrupe los datos `x` e `y`, y funciones externas que operen sobre ese `struct`. La operación de calcular la distancia al origen se implementa como una función que recibe un puntero (o una copia) al `struct` y devuelve el resultado. De este modo, se separan **datos** (en el `struct`) y **comportamiento** (en funciones), ya que C no asocia métodos a tipos de forma nativa. Una convención útil es anteponer el nombre del “tipo” al de la función, por ejemplo `Punto_calculaDistanciaAOrigen`, para simular el espacio de nombres propio de una clase.

### Respecto a `this`, en C **no existe** referencia implícita al objeto actual. Lo que en Java sería `this` pasa a ser un **parámetro explícito**: un puntero al `struct` (`Punto*`) que se pasa a cada función que actúa “como método”. Por ejemplo, `double Punto_calculaDistanciaAOrigen(const Punto* p)` usa `p->x` y `p->y` para acceder a sus campos. Si se desea emular aún más el estilo OO, pueden usarse **punteros a función** dentro del `struct`, aunque suele ser innecesario para ejemplos simples. También pueden añadirse funciones “constructoras” tipo `Punto Punto_crear(double x, double y)` o inicializadoras `void Punto_init(Punto* p, double x, double y)`.

```c
/* Punto.h */
#ifndef PUNTO_H
#define PUNTO_H

typedef struct {
    double x;
    double y;
} Punto;

/* “Constructor” por conveniencia */
static inline Punto Punto_crear(double x, double y) {
    Punto p = { x, y };
    return p;
}

/* “Método”: distancia al origen */
double Punto_calculaDistanciaAOrigen(const Punto* p);

#endif /* PUNTO_H */
```

```c
/* Punto.c */
#include <math.h>
#include "Punto.h"

double Punto_calculaDistanciaAOrigen(const Punto* p) {
    /* Equivalente a Math.sqrt(x*x + y*y) */
    return sqrt((p->x * p->x) + (p->y * p->y));
}
```

```c
/* main.c */
#include <stdio.h>
#include "Punto.h"

int main(void) {
    Punto p = Punto_crear(3.0, 4.0);

    double d = Punto_calculaDistanciaAOrigen(&p);
    printf("Distancia al origen: %.2f\n", d); /* Imprime 5.00 */

    return 0;
}
```

### En este patrón, el parámetro `const Punto* p` hace el papel de `this`: se pasa de forma explícita y se accede a los campos con `p->x` y `p->y`. No hay encapsulamiento, herencia ni métodos reales; solo **datos + funciones** con una convención de nombres que ayuda a organizar el código y a reducir la “magia” que ofrecen los lenguajes orientados a objetos.


<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Encapsulación". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
## TEMA 2. Encapsulación

##### 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.

##### 
La **encapsulación** y la **ocultación de información** buscan limitar el acceso directo al estado interno de los objetos, permitiendo que solo se interactúe con ellos a través de métodos definidos por la clase. De este modo, se separa claramente qué partes son internas y cuáles forman la interfaz pública, evitando dependencias innecesarias y reduciendo errores derivados de modificaciones no controladas.

Entre las ventajas de la ocultación de información destaca la **protección del estado interno**, ya que impide que el código externo altere atributos de manera incorrecta o incoherente. Además, favorece la **modularidad**, permitiendo que el código externo utilice una clase sin conocer su implementación. Esto también facilita la **evolución y mantenimiento** del software, ya que los cambios internos no afectan a quienes usan la clase mientras la interfaz pública se mantenga estable.



##### 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

### 
La **interfaz pública** de una clase u objeto se entiende como el conjunto de métodos y, en menor medida, constantes accesibles desde el exterior. Representa aquello que otros componentes del programa pueden utilizar para interactuar con la clase sin necesidad de conocer cómo están implementados sus detalles internos. En lenguajes como Java, esta interfaz se define normalmente mediante miembros declarados como `public`, que constituyen el “contrato” que la clase ofrece a cualquier código que quiera usarla.

Esta interfaz pública está estrechamente relacionada con la **ocultación de información**, ya que actúa como frontera entre lo que se expone y lo que se protege. Al mantener los atributos como `private` y ofrecer únicamente los métodos necesarios, se evita que el código externo pueda manipular directamente el estado interno del objeto. De esta forma, la clase conserva el control sobre cómo se accede y modifica su información, permitiendo cambiar la implementación interna sin afectar a quienes usan la interfaz pública.



##### 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

La **interfaz pública** debe diseñarse con cuidado porque actúa como el “contrato” que la clase ofrece al exterior. Todo el código que use esa clase dependerá directamente de esa interfaz, por lo que cualquier cambio puede afectar a múltiples partes del programa. Un diseño poco pensado puede obligar a exponer métodos innecesarios o permitir usos incorrectos del objeto, dificultando su mantenimiento y aumentando el riesgo de errores.

Cambiar la interfaz pública **no suele ser fácil**. Una vez que otros componentes del sistema dependen de ella, modificar nombres de métodos, parámetros o comportamientos implica ajustar todo el código que la utiliza. Por ello, es preferible mantener estables las partes públicas y dejar que los cambios internos ocurran dentro de la implementación privada, preservando la compatibilidad y reduciendo el impacto en el resto del programa.



##### 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

Las **invariantes de clase** son condiciones que deben cumplirse siempre para que un objeto se considere en un estado válido. Suelen referirse a relaciones lógicas entre los atributos, como límites, coherencia entre valores o reglas internas que la clase debe respetar en todo momento excepto durante la ejecución interna de algunos métodos. Estas invariantes permiten razonar sobre el comportamiento del objeto y garantizan que funcione de forma predecible.

La **ocultación de información** ayuda a mantener estas invariantes porque evita que el exterior modifique directamente los atributos. Al obligar a que cualquier cambio pase por métodos controlados, la propia clase puede verificar, corregir o impedir modificaciones que violen sus reglas internas. De este modo, la implementación puede asegurar que el objeto nunca quede en un estado inconsistente y que sus invariantes se mantengan automáticamente.


##### 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

A continuación, un ejemplo que usa **ocultación de información** manteniendo los atributos privados y exponiendo solo lo necesario en la interfaz pública:

```java
public class Punto {
    // Estado interno oculto
    private double x;
    private double y;

    // Constructor (parte de la interfaz pública)
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    // Métodos de acceso controlado (interfaz pública)
    public double getX() { return x; }
    public double getY() { return y; }
    public void setX(double x) { this.x = x; }
    public void setY(double y) { this.y = y; }

    // Comportamiento expuesto (interfaz pública)
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    // Ejemplo de método interno (podría ser private si hiciera falta)
    private double cuadrado(double v) { return v * v; }
}
```

La **interfaz pública** de `Punto` está formada por lo que se puede usar desde fuera: el **constructor `Punto(double, double)`**, los **getters** `getX()`, `getY()`, los **setters** `setX(double)`, `setY(double)`, y el método **`calcularDistanciaAOrigen()`**. El estado (`x`, `y`) se mantiene **`private`** para impedir modificaciones directas y preservar invariantes como “las coordenadas son números reales válidos” o cualquier regla futura sin romper el código cliente.

En Java, **`public`** significa **accesible desde cualquier clase** (el método/constructor forma parte del contrato externo). **`private`** significa **accesible solo desde dentro de la propia clase**, permitiendo ocultar detalles de implementación y forzar que cualquier cambio del estado pase por métodos controlados. Esta separación facilita el mantenimiento y permite cambiar la implementación interna sin afectar a quien usa la clase.



##### 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

En Java, los modificadores de acceso **`public`** y **`private`** se aplican a **miembros de clase** (métodos, campos y constructores) y a **clases anidadas** (clases e interfaces definidas dentro de otra clase). Así, un método `public` es accesible desde cualquier código, mientras que uno `private` solo es accesible dentro de la propia clase. Los **constructores** pueden ser `private` para restringir la creación de instancias (p. ej., en *singletons* o *factories*). Las **clases anidadas** pueden ser `public` o `private` para controlar su visibilidad respecto a la clase contenedora.

En cambio, las **clases de nivel superior** (top‑level) **no pueden ser `private`**: solo pueden ser `public` o tener acceso por defecto (*package‑private*, sin modificador). De forma similar, **paquetes, parámetros y variables locales** no admiten `public`/`private`. Las **interfaces y `enum` de nivel superior** siguen la misma regla que las clases top‑level (pueden ser `public` o *package‑private*); sus **miembros** pueden usar `public`/`private` según corresponda (teniendo en cuenta que los miembros de interfaz son `public static final` y los métodos son `public` por defecto).



##### 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

En POO existen más niveles de visibilidad además de la pública y la privada. La idea general es ofrecer distintos grados de acceso para controlar mejor qué partes de una clase pueden usarse desde fuera y cuáles quedan restringidas. Muchos lenguajes incorporan niveles intermedios para dar más flexibilidad a la hora de diseñar APIs y mantener encapsulado el comportamiento interno.

En **Java**, además de `public` y `private`, existen **dos niveles adicionales**:

*   **`protected`**, que permite el acceso desde la propia clase, desde clases del mismo paquete y desde subclases incluso si están en otro paquete.
*   **package‑private** (por defecto, sin escribir modificador), que permite el acceso solo desde clases del mismo paquete. Este nivel funciona como un término medio útil cuando se quiere permitir colaboración interna entre clases relacionadas, pero sin hacer pública una funcionalidad.

En **otros lenguajes**, la variedad es mayor. Por ejemplo, **C++** combina `public`, `private` y `protected` tanto para herencia como para miembros, y permite un control más granular. Lenguajes como **C#** añaden niveles adicionales como `internal` (visible solo dentro del ensamblado) o `protected internal`, que mezcla características de ambos. Otros lenguajes, como **Python**, siguen un enfoque más informal basado en convenciones, donde el encapsulamiento no se impone mediante el compilador, sino por acuerdos de estilo como el uso de guiones bajos para indicar miembros “privados”.



##### 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

La ocultación de miembros **privados** afecta a **otras clases** (a), no a **otras instancias de la misma clase** (b). En Java, el código que está **dentro de la misma clase** puede acceder a los campos privados de **cualquier instancia** de esa clase, no solo a los de `this`. Por tanto, los privados están ocultos para el exterior (otras clases), pero **no** entre objetos del **mismo tipo**, ya que comparten el mismo ámbito de clase.

Ejemplo con `calcularDistanciaAPunto(Punto otro)`, accediendo legalmente a `otro.x` y `otro.y` aunque sean `private`, por estar dentro de la propia clase `Punto`:

```java
public class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    public double calcularDistanciaAPunto(Punto otro) {
        // Acceso válido: estamos dentro de la clase Punto
        double dx = this.x - otro.x;
        double dy = this.y - otro.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}
```

En consecuencia, la respuesta correcta es que los miembros privados están **ocultos para otras clases** (a), pero **no** para otras instancias de la **misma clase** (b). Esto permite implementar lógica que compare o combine estados de dos objetos del mismo tipo respetando la encapsulación hacia el exterior, manteniendo a la vez la flexibilidad de implementación dentro de la clase.



##### 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

Los métodos **getter** y **setter** son funciones diseñadas para **acceder** y **modificar** atributos privados de un objeto respetando la encapsulación. Un *getter* devuelve el valor de un atributo, mientras que un *setter* permite actualizarlo de forma controlada. Se emplean cuando el estado interno está declarado como `private`, de modo que el acceso directo queda prohibido desde fuera de la clase.

Los *getters* permiten consultar información sin exponer los detalles internos de cómo se almacena, lo que ayuda a mantener una interfaz estable aunque la implementación cambie. Los *setters* ofrecen un punto de control para validar o restringir cambios, permitiendo mantener invariantes de clase y evitar estados inconsistentes. Así, ambos métodos actúan como una “puerta de acceso” al estado del objeto, asegurando que cualquier operación se realice de manera segura y coherente con el diseño de la clase.



##### 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

Cuando se dice que la **ocultación de información mejora la “seguridad”**, no se está hablando de seguridad frente a *hackers* ni de protección contra ataques externos. En este contexto, “seguridad” se refiere a la **robustez interna del programa**, es decir, a evitar que el propio código cometa errores al acceder o modificar datos que deberían estar controlados. La encapsulación actúa como una barrera lógica que impide que partes no autorizadas del programa alteren el estado interno de un objeto de forma incorrecta.

Gracias a esta ocultación, el estado se modifica únicamente a través de métodos controlados, lo que permite mantener invariantes, validar datos y garantizar coherencia en el comportamiento. Esto reduce fallos y facilita el mantenimiento del programa, pero **no** constituye una medida de seguridad en el sentido criptográfico o de protección ante ataques maliciosos. Por tanto, se trata de una forma de seguridad **interna y estructural**, no de protección frente a intrusiones externas.



##### 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

Un **miembro de instancia** es aquel que pertenece a cada objeto individual creado a partir de una clase. Cada instancia tiene su propia copia de esos atributos y métodos, de modo que su valor puede variar entre objetos. En cambio, un **miembro de clase** (declarado con `static` en Java) pertenece a la **clase en sí**, no a los objetos, por lo que existe una única copia compartida por todas las instancias. Esto permite almacenar información común, como contadores o constantes, sin necesidad de duplicarla en cada objeto.

Ambos tipos de miembros pueden **ocultarse** utilizando modificadores como `private`. Un atributo o método `static` puede ser privado igual que uno de instancia, y quedará accesible solo dentro de la propia clase. Esto es útil cuando se quiere encapsular lógica o datos globales que forman parte de la implementación interna de la clase, evitando que el código externo dependa de detalles que no deben exponerse.

En general, la diferencia clave reside en el **ámbito al que pertenecen** (objeto frente a clase), mientras que la capacidad de aplicar ocultación no cambia; tanto miembros de instancia como de clase pueden controlarse mediante `private`, `public` y los demás niveles de visibilidad disponibles en Java.



##### 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

Sí, tiene sentido que los **constructores sean privados** en ciertos diseños. Un constructor privado evita que otras clases puedan crear instancias directamente, lo que permite controlar completamente cómo y cuándo se generan los objetos. Este enfoque es útil cuando se quiere restringir la creación de instancias o garantizar que solo existan ciertos objetos válidos.

Un caso típico es el **patrón Singleton**, en el que solo debe existir una instancia de la clase. Otro caso es cuando la clase proporciona **métodos estáticos de creación** (*factory methods*), que permiten decidir qué tipo de objeto devolver, validar parámetros o reutilizar instancias ya existentes. También resulta útil en clases que no deben instanciarse nunca, como utilidades con métodos estáticos.

En estos escenarios, el constructor privado forma parte de la implementación interna y contribuye a mantener la estructura del programa clara y controlada, evitando usos indebidos desde el exterior.



##### 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

En Java, los **miembros de clase** se indican con el modificador `static`. Pertenecen a la **clase** y no a cada instancia, por lo que existe una única copia compartida. Son adecuados para mantener estado o utilidades comunes a todos los objetos. Igual que los miembros de instancia, pueden combinarse con modificadores de visibilidad (`public`, `private`, etc.) y con `final` cuando se trate de constantes.

Ejemplo ampliando la clase `Punto` para registrar los **máximos globales** de `x` e `y` observados en todas las instancias creadas o modificadas. Se usan campos estáticos privados y métodos estáticos públicos para consultarlos; el constructor y los *setters* actualizan estos máximos:

```java
public class Punto {
    // Estado interno (instancia)
    private double x;
    private double y;

    // Miembros de clase (compartidos por todas las instancias)
    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
        actualizarMaximos(x, y);
    }

    public double getX() { return x; }
    public double getY() { return y; }

    public void setX(double x) {
        this.x = x;
        actualizarMaximos(this.x, this.y);
    }

    public void setY(double y) {
        this.y = y;
        actualizarMaximos(this.x, this.y);
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    public double calcularDistanciaAPunto(Punto otro) {
        double dx = this.x - otro.x;
        double dy = this.y - otro.y;
        return Math.sqrt(dx * dx + dy * dy);
    }

    // Getters de clase (interfaz pública para los máximos globales)
    public static double getMaxX() { return maxX; }
    public static double getMaxY() { return maxY; }

    // Implementación interna para mantener los máximos
    private static void actualizarMaximos(double x, double y) {
        if (x > maxX) maxX = x;
        if (y > maxY) maxY = y;
    }
}
```

Con este diseño, `Punto.getMaxX()` y `Punto.getMaxY()` devuelven los valores máximos **globales** vistos hasta el momento, independientemente de la instancia desde la que se llamen. Nótese que `maxX` y `maxY` están **ocultos** (`private`) y solo son accesibles a través de la **interfaz pública estática**, preservando la encapsulación.



##### 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

Aquí tienes el método factoría solicitado. Incluye el redondeo y **sí**, debe usarse `static`, porque un método factoría pertenece a la **clase**, no a una instancia concreta:

```java
public static Punto crearRedondeado(double x, double y) {
    long rx = Math.round(x);
    long ry = Math.round(y);
    return new Punto(rx, ry);
}
```

Este método construye un nuevo `Punto` a partir de las coordenadas redondeadas al entero más cercano y devuelve la instancia creada.



##### 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

A continuación se muestra una versión de `Punto` que **mantiene la misma interfaz pública** (constructor, getters/setters y métodos de distancia), pero sustituye los dos `double` por un **array interno** de dos posiciones. La ocultación de información permite cambiar la representación interna sin afectar al código cliente que ya usa la clase.

Se preservan los nombres y firmas de los métodos para no romper dependencias. Internamente, `coords[0]` representa `x` y `coords[1]` representa `y`. Este cambio ilustra cómo la encapsulación permite evolucionar la implementación sin modificar la interfaz pública.

```java
public class Punto {
    // Representación interna: array de tamaño 2 -> [x, y]
    private final double[] coords = new double[2];

    // Constructor público (interfaz pública intacta)
    public Punto(double x, double y) {
        this.coords[0] = x; // x
        this.coords[1] = y; // y
    }

    // Getters públicos (interfaz pública intacta)
    public double getX() { return coords[0]; }
    public double getY() { return coords[1]; }

    // Setters públicos (interfaz pública intacta)
    public void setX(double x) { coords[0] = x; }
    public void setY(double y) { coords[1] = y; }

    // Comportamiento expuesto (interfaz pública intacta)
    public double calcularDistanciaAOrigen() {
        double x = coords[0], y = coords[1];
        return Math.sqrt(x * x + y * y);
    }

    public double calcularDistanciaAPunto(Punto otro) {
        double dx = this.coords[0] - otro.coords[0];
        double dy = this.coords[1] - otro.coords[1];
        return Math.sqrt(dx * dx + dy * dy);
    }

    // Si hubiera métodos de clase o factorías previas, pueden mantenerse sin cambios
    // porque no dependen de la representación interna.
}
```



##### 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

Aunque un atributo tenga *getter* y *setter* públicos, no es mejor declararlo público. Mantenerlo **privado** permite conservar el control sobre su acceso, validar valores en el *setter* o cambiar la representación interna sin afectar a quienes usan la clase. Si el atributo fuera público, cualquier código podría modificarlo libremente, impidiendo proteger el estado interno y dificultando la evolución de la implementación.

La convención más habitual en lenguajes orientados a objetos como Java es que **todos los atributos sean privados** y que el acceso se realice mediante métodos públicos. Esta práctica estandariza la encapsulación, evita exponer detalles internos y permite añadir lógica adicional en el futuro sin romper el código cliente. Incluso si hoy los *getters* y *setters* solo devuelven y asignan valores, mañana podrían incluir validaciones o mantener invariantes sin alterar la interfaz pública.

Esto está directamente relacionado con las **invariantes de clase**, ya que estas requieren que el estado del objeto permanezca siempre en condiciones válidas. Al mantener los atributos privados, es la propia clase quien controla cualquier modificación, lo que permite garantizar que las invariantes se cumplan automáticamente. Si los atributos fueran públicos, cualquiera podría cambiarlos libremente y dejar el objeto en un estado inconsistente, rompiendo dichas invariantes.



##### 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

Una clase **inmutable** es aquella cuyo estado no puede modificarse después de ser creada. Todos sus atributos permanecen constantes, normalmente declarados como `private` y `final`, y la clase no ofrece métodos que alteren ese estado. Si se necesita un “cambio”, se devuelve un **nuevo objeto**, en lugar de modificar el existente. De este modo, cada instancia representa un valor fijo y coherente durante toda su vida.

Un **método modificador** es cualquier método que cambie el estado interno de un objeto. Aunque a veces coincide con un *setter*, **no todo modificador es un setter**: cualquier método que altere atributos —aunque no se llame `set…`— es un modificador. Por ejemplo, un método `mover(double dx, double dy)` que cambie las coordenadas de un punto también es un modificador, aunque no tenga la forma típica de un *setter*.

Las clases inmutables tienen varias ventajas. Facilitan el razonamiento, ya que sus objetos nunca cambian y no pueden entrar en estados inconsistentes. También son más seguras en entornos concurrentes, porque varios hilos pueden usarlas sin riesgo de interferencias. Además, permiten mantener invariantes de clase de forma más sencilla: si el estado no cambia, es más fácil garantizar que siempre se cumplen. Por estas razones, muchos lenguajes y bibliotecas utilizan ampliamente la inmutabilidad para diseñar tipos fiables y fáciles de mantener.



##### 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

No, no es recomendable incluir métodos *setter* siempre ni tomarlos como una convención obligatoria. Incluir *setters* sin necesidad puede debilitar la encapsulación, ya que expone más puntos de modificación del estado del objeto y obliga a que la clase mantenga un diseño más abierto del necesario. Cuando se añaden *setters* por rutina, se pierde la oportunidad de controlar adecuadamente cómo y cuándo puede cambiar el estado, lo que puede facilitar la aparición de errores o estados inconsistentes.

Lo más habitual en diseño orientado a objetos es **no exponer setters a menos que realmente sean necesarios**. Muchos atributos deberían ser solo de lectura, especialmente si representan información que no debería cambiar después de la construcción del objeto. Además, en modelos donde la inmutabilidad aporta claridad o seguridad, la ausencia de setters es esencial, ya que ayuda a preservar invariantes y simplifica el razonamiento sobre el estado del objeto.

En definitiva, la decisión de incluir un *setter* debe basarse en la necesidad real de modificar un atributo desde fuera. Si no es necesario, es preferible no proporcionarlo. Esto mejora la encapsulación, limita el acoplamiento con otros componentes y permite que la clase evolucione sin romper su interfaz pública ni comprometer sus invariantes internas.



##### 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

La clase **`String`** en Java es **inmutable**, lo que significa que una vez creada no puede modificar su contenido interno. Cualquier operación que parezca cambiar una cadena en realidad crea un **nuevo objeto `String`**, manteniendo intacto el original. Esto facilita preservar invariantes, evita estados inconsistentes y simplifica el razonamiento en programas concurrentes.

Al **concatenar dos cadenas**, Java no modifica ninguna de ellas, sino que construye **una nueva cadena** con el resultado. Por ejemplo, `s = s + "a";` crea internamente un nuevo objeto `String` y asigna su referencia a `s`. Este proceso puede ser costoso si se realiza repetidamente en un bucle, porque se generan muchos objetos temporales en memoria, implicando sobrecarga y trabajo adicional para el recolector de basura.

Cuando se necesita construir una cadena **mediante muchas concatenaciones**, la práctica recomendada es usar **`StringBuilder`** (o `StringBuffer` si hay concurrencia). Estas clases son **mutables**, lo que permite añadir fragmentos sin crear nuevos objetos en cada operación. Al finalizar, se convierte el resultado a `String` mediante `toString()`, obteniendo así una solución eficiente tanto en tiempo como en memoria.



##### 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

En POO, los objetos pueden compararse por **identidad** (si son exactamente el mismo objeto en memoria) o por **contenido** (si representan la misma información). En Java, el operador `==` compara **identidad**, es decir, si dos referencias apuntan al **mismo objeto**. Para comparar contenido, se recurre a un método específico que cada clase puede redefinir según sus necesidades semánticas.

Ese método es **`equals`**, heredado de `Object`. Por defecto, `equals` **se comporta igual que `==`**, comparando identidad y no contenido. Para que dos objetos se consideren “iguales” por su información interna, una clase debe **sobrescribir `equals`** e implementar la comparación lógica adecuada. Esto permite que dos instancias distintas, pero con el mismo estado, se consideren equivalentes desde el punto de vista del programa.

En el caso de las cadenas, **dos `String` deben compararse con `equals`**, nunca con `==`. El operador `==` solo diría si son el mismo objeto, mientras que `equals` compara carácter por carácter. Por tanto, expresiones como `"hola".equals(otraCadena)` son la manera correcta y segura de comparar cadenas en Java.



##### 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

Las **clases *wrapper*** son clases que envuelven (*wrap*) un tipo primitivo para tratarlo como un **objeto** en lenguajes orientados a objetos. En Java, cada tipo primitivo tiene su correspondiente *wrapper*: `int → Integer`, `double → Double`, `boolean → Boolean`, etc. Estas clases permiten usar valores primitivos allí donde se requieren objetos, por ejemplo, en colecciones genéricas como `ArrayList`, que no pueden almacenar tipos primitivos directamente. La conversión se hace creando una instancia del *wrapper* que contiene el valor primitivo en su interior.

En Java, este proceso puede hacerse de manera **explícita** (por ejemplo, `new Integer(5)` o `Integer.valueOf(5)`), pero normalmente es **automático** gracias a *autoboxing* y *unboxing*. Autoboxing convierte un primitivo en su wrapper cuando es necesario, mientras que el unboxing hace la operación inversa. De esta forma, expresiones como `Integer x = 5;` o `int y = x;` funcionan sin que el programador tenga que escribir conversiones manuales. Este mecanismo facilita el uso combinado de primitivos y objetos, manteniendo un código más limpio y expresivo.

Las clases wrapper ofrecen varias ventajas. Permiten almacenar valores primitivos en colecciones, aportar métodos adicionales (por ejemplo, parsers o utilidades), y representar valores nulos, algo que un primitivo no puede hacer. Asimismo, contribuyen a una mayor integración con el diseño orientado a objetos, donde muchas API trabajan exclusivamente con tipos de referencia. Gracias a ellas, es posible tratar valores numéricos o booleanos como objetos con comportamiento adicional cuando el diseño lo requiere.

No todos los lenguajes orientados a objetos necesitan wrappers. Algunos lenguajes no tienen **tipos primitivos** separados y tratan los números o booleanos directamente como objetos —por ejemplo, Python o Ruby—, eliminando la necesidad de envoltorios específicos. Otros lenguajes, como Java o C#, sí distinguen entre primitivos y objetos por razones de eficiencia, lo que lleva a la existencia de wrappers para integrar ambos mundos.



##### 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

Un **tipo de dato enumerado** en POO es un conjunto finito y cerrado de valores posibles que representan opciones claramente definidas. Se usa cuando un dato solo puede pertenecer a un pequeño grupo de alternativas válidas, lo que ayuda a evitar errores y a expresar el significado del programa de forma más precisa. Conceptualmente, un enumerado define un tipo propio cuyos valores son constantes simbólicas.

En **Java**, un tipo enumerado (`enum`) es efectivamente una **clase especial**, aunque con una sintaxis más compacta y un comportamiento predeterminado. Detrás de la sintaxis del `enum`, Java genera una clase final con un número fijo de instancias predefinidas y públicas. Esto implica que cada valor del `enum` es un **objeto único** y que no pueden crearse nuevas instancias fuera del propio tipo, garantizando así la integridad del conjunto de valores posibles.

Los enumerados en Java ofrecen ventajas importantes en términos de **encapsulación**. Permiten añadir **métodos**, **atributos privados**, e incluso redefinir comportamientos para cada valor, manteniendo todo el funcionamiento relacionado dentro del propio `enum`. También evitan que partes externas creen valores no permitidos, ya que el constructor de un `enum` es siempre privado. Gracias a esto, los enumerados refuerzan la seguridad del tipo, aseguran la validez de sus valores y permiten que los detalles internos evolucionen sin afectar a quienes lo utilizan.



##### 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.

Aquí tienes un tipo enumerado `Mes` completo, usando **atributos privados**, **constructor privado** y **métodos públicos** para obtener el número de días y el ordinal del mes. El código cumple con las reglas de encapsulación típicas de los `enum` en Java.

```java
public enum Mes {

    ENERO(31, 1),
    FEBRERO(28, 2),
    MARZO(31, 3),
    ABRIL(30, 4),
    MAYO(31, 5),
    JUNIO(30, 6),
    JULIO(31, 7),
    AGOSTO(31, 8),
    SEPTIEMBRE(30, 9),
    OCTUBRE(31, 10),
    NOVIEMBRE(30, 11),
    DICIEMBRE(31, 12);

    // Atributos privados de cada instancia del enum
    private final int dias;
    private final int numeroMes;

    // Constructor privado (implícitamente privado en los enums)
    Mes(int dias, int numeroMes) {
        this.dias = dias;
        this.numeroMes = numeroMes;
    }

    // Método público para obtener los días que tiene el mes
    public int getDias() {
        return dias;
    }

    // Método público para obtener el número de mes (1-12)
    public int getNumeroMes() {
        return numeroMes;
    }
}
```

Este `enum` encapsula correctamente la información:

*   Cada mes es una **instancia única** creada por Java.
*   Los atributos son **privados y finales**, reforzando la inmutabilidad.
*   La lógica relacionada con el concepto de “mes” queda agrupada en el tipo enumerado.

Si necesitas añadir métodos como “¿es trimestre 1?”, “¿es verano?”, etc., se podrían incorporar sin cambiar el modo de uso del `enum`.



##### 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

Se consideran las **estaciones astronómicas estándar** por meses completos: en el **hemisferio norte**, primavera (3–5), verano (6–8), otoño (9–11) e invierno (12–2). En el **hemisferio sur** se invierten: primavera (9–11), verano (12–2), otoño (3–5) e invierno (6–8). Aunque en la realidad comienzan/terminan alrededor de los solsticios/equinoccios, por simplicidad se asigna el mes completo a una estación.

A continuación se añaden los cuatro métodos a `Mes` usando el ordinal 1–12 almacenado en `numeroMes`. Se mantiene la encapsulación al no exponer nuevos detalles internos y ofrecer una interfaz clara:

```java
public boolean esDePrimavera(boolean esHemisferioNorte) {
    int m = this.getNumeroMes();
    if (esHemisferioNorte) {
        return m >= 3 && m <= 5;       // Mar, Abr, May
    } else {
        return m >= 9 && m <= 11;      // Sep, Oct, Nov
    }
}

public boolean esDeVerano(boolean esHemisferioNorte) {
    int m = this.getNumeroMes();
    if (esHemisferioNorte) {
        return m >= 6 && m <= 8;       // Jun, Jul, Ago
    } else {
        return m == 12 || m <= 2;      // Dic, Ene, Feb
    }
}

public boolean esDeOtoño(boolean esHemisferioNorte) {
    int m = this.getNumeroMes();
    if (esHemisferioNorte) {
        return m >= 9 && m <= 11;      // Sep, Oct, Nov
    } else {
        return m >= 3 && m <= 5;       // Mar, Abr, May
    }
}

public boolean esDeInvierno(boolean esHemisferioNorte) {
    int m = this.getNumeroMes();
    if (esHemisferioNorte) {
        return m == 12 || m <= 2;      // Dic, Ene, Feb
    } else {
        return m >= 6 && m <= 8;       // Jun, Jul, Ago
    }
}
```


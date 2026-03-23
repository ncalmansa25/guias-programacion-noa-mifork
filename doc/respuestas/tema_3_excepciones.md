# TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.

### Respuesta

Una primera opción clásica en C consiste en **devolver un código de error** (por ejemplo, `int`) y **entregar el resultado por parámetro de salida** (puntero). De este modo, la función no mezcla el valor de retorno con el estado de error y el llamador decide qué hacer (imprimir un mensaje, abortar, etc.). Es el patrón que se ve con frecuencia en librerías de C.

```c
#include <math.h>
#include <stdio.h>

int raiz(double x, double* out) {
    if (x < 0.0) return -1;     // código de error
    *out = sqrt(x);
    return 0;                   // éxito
}

int main(void) {
    double r;
    if (raiz(-9.0, &r) != 0) {
        printf("Error: argumento negativo\n");
    } else {
        printf("Resultado: %f\n", r);
    }
}
```

Una segunda opción es **usar `errno` y/o valores centinela** (por ejemplo, `NAN` de `<math.h>`) para señalar errores. Este enfoque permite consultar la causa mediante `errno` y constantes como `EDOM` (dominio inválido). El llamador comprueba `isnan()` y, si procede, mira `errno` y decide cómo informar.

```c
#include <math.h>
#include <errno.h>
#include <stdio.h>
#include <fenv.h>

double raiz(double x) {
    if (x < 0.0) {
        errno = EDOM;           // dominio matemático inválido
        return NAN;             // centinela
    }
    errno = 0;
    return sqrt(x);
}

int main(void) {
    errno = 0;
    double r = raiz(-4.0);
    if (errno == EDOM || isnan(r)) {
        printf("Error: argumento negativo (errno=%d)\n", errno);
    } else {
        printf("Resultado: %f\n", r);
    }
}
```

***

## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?

### Respuesta

Una **excepción** es un mecanismo del lenguaje que permite **señalizar y transportar** condiciones anómalas o situaciones de error desde el punto donde se detectan hasta un manejador situado en otra parte del programa. En lugar de codificar y propagar manualmente códigos de error, una excepción interrumpe el flujo normal y transfiere el control a un bloque que sabe gestionarla.

Se utilizan al **implementar** funciones para **separar la lógica normal** de la **gestión de fallos**, manteniendo el código más legible y evitando comprobaciones repetitivas tras cada llamada. Al **llamar** funciones, se emplean para **centralizar el manejo** (por ejemplo, en un nivel superior de la aplicación), decidiendo si se recupera, se informa al usuario o se aborta la operación, sin contaminar el flujo principal con ramificaciones de error en cada línea.

***

## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

### Respuesta

En Java, se puede modelar el error de argumento negativo como un **fallo de precondición**, lanzando una `IllegalArgumentException` (no controlada) desde el método `raiz`. La clase `Calculadora` encapsula la operación y su contrato.

```java
public class Calculadora {
    public static double raiz(double x) {
        if (x < 0) {
            throw new IllegalArgumentException("x debe ser no negativo");
        }
        return Math.sqrt(x);
    }

    public static void main(String[] args) {
        try {
            double r = Calculadora.raiz(-9);
            System.out.println("Resultado: " + r);
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

El **control** del error se realiza desde fuera, en el `main`, con un bloque `try-catch` que captura la excepción y decide cómo informar. La lógica normal permanece limpia y la validación queda localizada dentro del método.

***

## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.

### Respuesta

**Lanzar** una excepción consiste en **crear** un objeto de excepción y **interrumpir** el flujo con `throw`, iniciando la búsqueda de un manejador adecuado. **Capturar** o **controlar** es interceptar esa excepción en un bloque `catch` cuyo tipo coincide (o es supertipo), de modo que se ejecute el código de manejo y, después, el programa continúe tras el `try-catch`.

La **propagación** ocurre cuando no hay un `catch` en el marco actual: la excepción **desenrolla la pila** (stack unwinding), abandonando funciones una a una hasta encontrar un manejador. Los marcos abandonados **no se reanudan** donde se produjo la excepción; su ejecución termina y solo se ejecutan sus bloques `finally` si existen. Si ningún nivel la captura, el hilo termina con un error no controlado.

Aplicado al ejemplo, `Calculadora.raiz(-9)` hace `throw new IllegalArgumentException(...)`. Si `main` contiene un `try-catch(IllegalArgumentException e)`, se captura allí. Si en vez de `main` existieran llamadas intermedias (p. ej., `servicio()` → `calcula()` → `raiz()`), y ninguna tuviera `catch`, la excepción subiría hasta `main`. Las funciones intermedias no “retoman” la ejecución tras el punto donde ocurrió el fallo; simplemente se abandonan.

***

## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?

### Respuesta

La primera ventaja es que **el flujo normal queda limpio** de comprobaciones repetitivas y códigos de error; no es necesario propagar manualmente enteros de estado ni banderas tras cada llamada. Esto reduce **boilerplate** y el riesgo de **ignorar** errores de forma accidental, algo frecuente cuando se devuelven códigos que no se comprueban.

La segunda ventaja es que la propagación incluye **información contextual rica** (tipo de excepción, mensaje, pila) y garantiza la ejecución de **finalizadores** (`finally` o *try-with-resources*) durante el desenrollado. En C, el programador debe recordar e implementar manualmente la liberación de cada recurso en todos los caminos de error, lo que resulta proclive a fugas y estados inconsistentes.

***

## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?

### Respuesta

En Java, las excepciones son **objetos** que heredan de `Throwable` (`Exception` o `RuntimeException`). Al ser objetos, pueden encapsular **estado** (mensaje, causa, datos adicionales) y **comportamiento** (métodos), y organizan su tipología en **jerarquías**, lo que permite capturas específicas o genéricas mediante polimorfismo.

Esta naturaleza orientada a objetos facilita la **encapsulación del error**: se puede modelar un dominio con sus propias excepciones, ocultando detalles internos y exponiendo mensajes significativos. Por ello, sí tiene sentido crear **excepciones personalizadas** (por ejemplo, `NumeroNegativoException`) para expresar con precisión las reglas de negocio y separar los errores del dominio de los errores de programación.

***

## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?

### Respuesta

Un objeto excepción aporta, como mínimo, el **tipo** (clase concreta), un **mensaje descriptivo** y la **traza de pila** que indica el camino de llamadas hasta el punto del fallo. Además, suele incluir la **causa** (otra excepción encadenada) para no perder el rastro desde un nivel bajo a uno alto.

En C, al usar códigos de error o `errno`, normalmente solo se dispone de un **número** y quizá una cadena global (`strerror(errno)`), sin traza de pila automática ni tipado jerárquico. Al llegar a un manejador en Java, esa información rica permite **diagnosticar** y **registrar** con detalle el problema, favoreciendo la depuración y la observabilidad.

***

## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?

### Respuesta

En Java se pueden encadenar **múltiples `catch`** después de un `try` para manejar **tipos diferentes** de excepción. Además, existe la forma de **multi-catch** (`catch (IOException | SQLException e)`) para agrupar varios tipos que compartan el mismo tratamiento.

En tiempo de ejecución, **solo se ejecuta un `catch`**: el primero que **coincide** con el tipo lanzado (considerando la jerarquía). Por ello, el orden debe ir de **más específico** a **más general**, evitando que un `catch` genérico capture antes y oculte manejadores específicos posteriores.

***

## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

### Respuesta

En Java, el bloque `finally` se **ejecuta siempre** tras el `try` (y sus `catch`, si los hay), ocurra o no una excepción, lo que lo convierte en el lugar adecuado para **liberar recursos** (cerrar ficheros, conexiones, etc.). Así se garantiza la limpieza incluso si la excepción se propaga.

Con `catch`:

```java
BufferedReader br = null;
try {
    br = new BufferedReader(new FileReader("datos.txt"));
    System.out.println(br.readLine());
} catch (IOException e) {
    System.err.println("Error de E/S: " + e.getMessage());
} finally {
    if (br != null) {
        try { br.close(); } catch (IOException ignore) {}
    }
}
```

Sin `catch` (se limpia y **se propaga**):

```java
BufferedReader br = null;
try {
    br = new BufferedReader(new FileReader("datos.txt"));
    System.out.println(br.readLine());
} finally {
    if (br != null) {
        try { br.close(); } catch (IOException ignore) {}
    }
}
```

***

## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

### Respuesta

Sí, es válido escribir **`try`–`finally`** sin `catch`. En ese caso, el `finally` se ejecuta tras el `try` y, si se produjo una excepción, esta se **propaga después** de ejecutar el `finally`. Este patrón se utiliza cuando el método **no** desea manejar la excepción, pero **sí** quiere asegurar la liberación de recursos.

El `finally` se ejecuta **tanto si hay** como si **no hay** excepción y también **antes** de que un `return` haga salir del método. Solo situaciones extraordinarias (por ejemplo, `System.exit`, muerte del proceso o fallo fatal de la JVM) impedirían su ejecución. Por ello, no se debe depender del `finally` para lógica de negocio que no deba ejecutarse en esos casos extremos.

***

## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

### Respuesta

Las **controladas** (*checked*) son subclases de `Exception` **que no** derivan de `RuntimeException`; el compilador exige **declararlas** con `throws` o **capturarlas**. Las **no controladas** (*unchecked*) son subclases de `RuntimeException` (y `Error`); **no** es obligatorio declararlas ni capturarlas. `RuntimeException` agrupa errores de **programación** o violaciones de precondiciones que, en general, no se esperan recuperar localmente.

**Ejemplos típicos**:  
Controladas: `IOException`, `SQLException`, `ParseException`, `ClassNotFoundException`.  
No controladas: `IllegalArgumentException`, `NullPointerException`, `IndexOutOfBoundsException`, `ArithmeticException`.

**Cuándo preferir controladas (checked):**

*   Fallos **externos** recuperables (E/S, red, permisos).
*   Operaciones donde el **contrato** obliga a tratar explícitamente el fallo (abrir fichero, cargar clase).
*   Procesos por lotes donde se desea **reintentar** o degradar funcionalidad.
*   APIs públicas que necesitan **forzar** al consumidor a considerar el error.

**Cuándo preferir no controladas (unchecked):**

*   **Errores de programación** (precondiciones no cumplidas).
*   Estados imposibles según el **invariante** del objeto.
*   Fallos que no tienen una **recuperación razonable** local (p. ej., corrupción de datos internos).
*   Validaciones rápidas de argumentos en métodos públicos (`IllegalArgumentException`, `NullPointerException`).

***

## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

### Respuesta

`throws` es parte de la **firma** de un método e indica que este puede **propagar** una o más **excepciones controladas**. Su función es **declarativa**: comunica al llamador qué condiciones excepcionales deben manejarse y permite que la comprobación se realice en **tiempo de compilación**.

Se considera alternativa a **capturar** (con `try-catch`) porque, ante una excepción controlada, el método tiene **dos opciones**: o la **maneja** localmente, o la **declara** con `throws` para que un nivel superior decida. Esta segunda opción evita capturas de “relleno” sin lógica útil y fomenta que el manejo ocurra en el **lugar adecuado**.

***

## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

### Respuesta

Una opción es **leer** y devolver la primera línea del fichero, declarando `throws IOException` para **propagar** la excepción (incluida `FileNotFoundException`). El `finally` asegura el **cierre** del recurso incluso si se lanza una excepción durante la lectura.

```java
import java.io.*;

public class Ficheros {
    public static String leerPrimeraLinea(String ruta) throws IOException {
        BufferedReader br = null;
        try {
            br = new BufferedReader(new FileReader(ruta)); // puede lanzar FileNotFoundException
            return br.readLine();                          // puede lanzar IOException
        } finally {
            if (br != null) {
                try { br.close(); } catch (IOException ignore) {}
            }
        }
    }
}
```

El llamador deberá decidir si captura la `IOException` o la vuelve a declarar. Alternativamente, podría emplearse *try-with-resources* en el propio método, pero el requisito pedía mostrar `finally`.

***

## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

### Respuesta

Sí, **se puede** listar en `throws` una `RuntimeException`, pero es **opcional** y no añade obligación de captura: el compilador no la exige. Incluirla puede servir como **documentación** del contrato (advertir que puede lanzarse cierta `RuntimeException`), o para herramientas de análisis estático y generación de documentación.

El método llamador **no está obligado** a usar `try-catch` para una no controlada; solo debería hacerlo si **desea** tratar ese caso particular (p. ej., registrar y continuar, transformar la excepción, o devolver una respuesta alternativa). En caso contrario, tiene sentido dejar que **se propague** hasta un manejador global.

***

## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

### Respuesta

Se recomiendan **controladas** cuando el fallo es **previsible** y potencialmente **recuperable** por el cliente de la API (E/S, red, disponibilidad de recursos), y cuando se desea **forzar** explícitamente una decisión en el código llamador. Por el contrario, se recomiendan **no controladas** para **errores de programación** (violación de precondiciones, argumentos inválidos, mal uso de la API), donde el manejo local rara vez es sensato.

No todos los lenguajes distinguen ambas categorías. Java es de los pocos con **checked** y **unchecked**. Lenguajes como **C#, C++, Python, JavaScript** solo tienen **no controladas** (no verificadas por compilador). En esos lenguajes, la práctica habitual es usar **excepciones no controladas** y documentar las que pueden producirse, apoyándose en pruebas y convenciones para su manejo.

***

## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

### Respuesta

Tiene sentido **traducir** o **elevar** una excepción dentro de un `catch` cuando se desea ocultar detalles de bajo nivel y exponer un **tipo de dominio** más significativo. Este patrón mantiene el encapsulamiento y simplifica el contrato de capas superiores, sin perder la causa original.

También se puede **relanzar la misma excepción** capturada (con `throw e;`) cuando el manejador actual solo registra o añade contexto y decide que otro nivel debe tomar la decisión final. Resulta útil para **añadir logging**, métricas o limpiar recursos, pero dejar que la semántica del fallo se trate en un lugar centralizado.

```java
// Traducir excepción
try {
    servicioIO.leer();
} catch (IOException e) {
    throw new DatosIndisponiblesException("No fue posible leer los datos", e);
}

// Relanzar la misma excepción (añadiendo registro)
try {
    calcular();
} catch (IllegalStateException e) {
    System.err.println("Contexto X falló: " + e.getMessage());
    throw e; // se propaga la misma excepción
}
```

***

## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

### Respuesta

La **causa** es una excepción **encadenada** que explica el **origen** de otra de mayor nivel. En Java, se establece pasando la excepción original al **constructor** de la nueva o mediante `initCause`. De este modo, no se pierde el contexto de bajo nivel al elevar el error a un tipo más adecuado para la capa superior.

Al imprimir la traza con `printStackTrace()` o al dejar que la excepción no se capture, la salida muestra el mensaje y la pila de la excepción principal, seguida de una sección **“Caused by:”** con la traza de la causa y, si hubiera, causas anidadas adicionales.

```java
class DatosIndisponiblesException extends Exception {
    public DatosIndisponiblesException(String msg, Throwable cause) {
        super(msg, cause);
    }
}

try {
    // Capa baja
    Files.readAllBytes(Path.of("inexistente.dat")); // lanza IOException
} catch (IOException e) {
    // Capa alta
    throw new DatosIndisponiblesException("No se pudo cargar el recurso de datos", e);
}
```

De esta forma, al visualizar la traza se observará la excepción de alto nivel y, a continuación, la línea **“Caused by: java.io.IOException …”** con su propio recorrido de pila, facilitando el diagnóstico end-to-end.



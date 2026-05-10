***

## 1. Uso de `void*` en C y `Object` en Java para estructuras genéricas

En C, una forma habitual de simular estructuras de datos genéricas consiste en utilizar punteros de tipo `void*`. Este tipo de puntero puede apuntar a cualquier otro tipo de dato, ya que no tiene información de tipo asociada. De este modo, una estructura que internamente almacene un array de `void*` puede guardar direcciones de enteros, estructuras, floats u otros tipos sin distinción.

En Java ocurre algo conceptualmente parecido al emplear `Object`. Dado que todas las clases heredan implícitamente de `Object`, un array de `Object` puede almacenar referencias a instancias de cualquier clase. Esto permite crear, por ejemplo, una lista basada en un array de `Object` que pueda contener distintos tipos de objetos.

```c
/* C con void* */
void* datos[10];
int x = 5;
double y = 3.14;
datos[0] = &x;
datos[1] = &y;
```

```java
// Java con Object
Object[] datos = new Object[10];
datos[0] = "Hola";
datos[1] = 42;
datos[2] = 3.14;
```

***

## 2. Significado de programación genérica

La **programación genérica** consiste en escribir código que sea independiente del tipo concreto de datos sobre el que opera. El objetivo es reutilizar algoritmos y estructuras de datos evitando duplicar código para cada tipo distinto, manteniendo a la vez seguridad y claridad.

El ejemplo anterior basado en `void*` u `Object` puede considerarse un primer acercamiento a la genericidad, ya que permite trabajar con múltiples tipos usando una sola estructura. Sin embargo, se trata de una forma muy básica e incompleta de programación genérica, ya que el tipo real se pierde y no existe verificación automática de tipos en tiempo de compilación.

Por tanto, aunque conceptualmente apunta a la genericidad, no ofrece las garantías ni ventajas completas de los mecanismos de programación genérica que proporcionan lenguajes como Java o C++ mediante *generics* o *templates*.

***

## 3. Problemas de chequeo de tipos con `void*` y `Object`

El principal problema de emplear `void*` en C es que el compilador pierde completamente la información de tipo. Cada vez que se recupera un valor, el programador debe realizar conversiones explícitas, confiando en recordar correctamente qué tipo se almacenó en cada posición. Un error en esta conversión provoca comportamientos indefinidos y errores difíciles de detectar.

En Java, aunque `Object` mantiene cierta información en tiempo de ejecución, el compilador tampoco puede garantizar que un objeto recuperado del array tenga el tipo esperado. Es necesario aplicar *downcasting*, lo que puede provocar excepciones `ClassCastException` si el tipo real no coincide.

En ambos casos, el error no se detecta en tiempo de compilación, sino en ejecución. Esto reduce la seguridad del programa y aumenta la probabilidad de fallos, además de hacer el código más verboso y propenso a errores.

***

## 4. Parámetros de tipo

Los **parámetros de tipo** son una característica del lenguaje que permite definir clases, interfaces o métodos parametrizados por uno o varios tipos. En lugar de usar `Object` o `void*`, se introduce un nombre simbólico para el tipo (por ejemplo, `T`) que será sustituido por un tipo concreto cuando se utilice la clase o método.

Gracias a los parámetros de tipo, el compilador puede comprobar que se están usando los tipos correctos y evitar conversiones inseguras. Esto permite mantener la flexibilidad de la programación genérica sin renunciar al chequeo de tipos estático.

Los parámetros de tipo son, por tanto, el mecanismo que hace posible una programación genérica segura, expresiva y más fácil de mantener, especialmente en estructuras de datos reutilizables como listas, mapas o pares de valores.

***

## 5. Ejemplo de genericidad en C++ y Java

En **C++**, la programación genérica se implementa mediante *templates*. El compilador genera versiones específicas del código para cada tipo utilizado. En **Java**, se emplean *generics*, que proporcionan seguridad de tipos sin duplicar código fuente.

```cpp
// C++ con templates
#include <vector>
#include <string>
#include <iostream>

std::vector<std::string> v;
v.push_back("uno");
v.push_back("dos");

for (const std::string& s : v) {
    std::cout << s << std::endl;
}
```

```java
// Java con generics
import java.util.ArrayList;
import java.util.List;

List<String> lista = new ArrayList<>();
lista.add("uno");
lista.add("dos");

for (String s : lista) {
    System.out.println(s);
}
```

En ambos casos, el compilador garantiza que los elementos son del tipo `String`, evitando conversiones y errores de tipo en tiempo de ejecución.

***

## 6. Trabajo del compilador: Java vs C++

Cuando se instancia una clase genérica, el compilador realiza un tratamiento especial del código. En **C++**, cada uso de un *template* con un tipo distinto genera una versión concreta del código, proceso conocido como **instanciación de plantillas**. Esto ocurre completamente en tiempo de compilación.

En **Java**, el compilador aplica un mecanismo llamado **type erasure**. Los parámetros de tipo se eliminan tras la compilación y se sustituyen por `Object` (o por el límite superior correspondiente). El bytecode resultante contiene una sola versión de la clase.

La diferencia clave es que C++ mantiene los tipos genéricos también en tiempo de compilación y genera código especializado, mientras que Java prioriza compatibilidad y simplicidad del bytecode, trasladando parte del control de tipos al compilador.

***

## 7. Clase genérica `Par` en Java

Se puede definir una clase genérica `Par` con dos parámetros de tipo, lo que permite almacenar dos valores de tipos distintos sin perder seguridad. Cada parámetro de tipo representa uno de los valores almacenados.

```java
class Par<A, B> {
    private final A primero;
    private final B segundo;

    public Par(A primero, B segundo) {
        this.primero = primero;
        this.segundo = segundo;
    }

    public A getPrimero() { return primero; }
    public B getSegundo() { return segundo; }
}
```

Un uso típico consiste en devolver más de un resultado desde una función. Por ejemplo, una función puede calcular la media y la desviación típica de un array de `double` y devolver ambos valores en un `Par<Double, Double>`.

***

## 8. Métodos genéricos en Java

En Java, los parámetros de tipo no son exclusivos de las clases, sino que también pueden declararse a nivel de método. Esto permite escribir métodos genéricos independientes del tipo de la clase que los contiene.

```java
public static <T> T seleccionaUno(T a, T b) {
    return Math.random() < 0.5 ? a : b;
}
```

Frente a una versión que recibe dos `Object`, el método genérico evita el *downcasting* y garantiza que ambos argumentos sean del mismo tipo. El compilador impide, por ejemplo, pasar un `String` y un `Integer`, reforzando el chequeo de tipos y la claridad del código.

***

## 9. Restricciones en parámetros de tipo

En Java, los parámetros de tipo pueden tener **restricciones** mediante `extends`. Esto permite indicar que el tipo genérico debe ser, como mínimo, una subclase de otra clase o implementar una interfaz determinada, como `Number`.

Una solución simple consiste en usar directamente `Number` como tipo de las coordenadas. Esto permite usar distintos tipos numéricos, pero pierde precisión en el tipo concreto. La alternativa genérica refuerza el chequeo:

```java
class Punto<T extends Number> {
    private final T x, y;

    public Punto(T x, T y) {
        this.x = x;
        this.y = y;
    }

    public T getX() { return x; }
    public T getY() { return y; }
}
```

Tras el *type erasure*, el tipo real utilizado internamente por Java será `Number`, aunque el compilador se asegure de que el uso en el código fuente es coherente con `T`.

***

## 10. Comparación de las dos soluciones

Ambas soluciones permiten evitar duplicar código y trabajar con distintos tipos numéricos. Sin embargo, la solución sin genéricos permite crear un punto con una coordenada entera y otra real, ya que ambas son simplemente `Number`.

Con genéricos, se fuerza a que ambas coordenadas sean exactamente del mismo tipo. Esto refuerza el diseño y evita incoherencias cuando se espera homogeneidad en las coordenadas.

Además, en la solución sin genéricos `getX` devuelve un `Number`, mientras que en la versión genérica devuelve `T`, conservando información de tipo en el código fuente y evitando conversiones innecesarias.

***

## 11. Genericidad en interfaces `Punto`

Se puede añadir un parámetro de tipo a la interfaz `Punto` para indicar sobre qué subtipo es válida la operación de distancia. De este modo, se garantiza que la distancia solo se calcule entre puntos del mismo tipo.

```java
public interface Punto<T extends Punto<T>> {
    double distanciaA(T p);
}

public class Punto2D implements Punto<Punto2D> {
    private final double x, y;

    @Override
    public double distanciaA(Punto2D p) {
        return Math.sqrt(Math.pow(x - p.x, 2) + Math.pow(y - p.y, 2));
    }
}
```

Este enfoque elimina completamente la necesidad de `instanceof` y *downcasting*, trasladando el chequeo al compilador y haciendo el diseño más robusto y expresivo.

***

## 12. Covarianza, contravarianza e invariancia

Aunque `String` sea subtipo de `Object`, **`List<String>` no es subtipo de `List<Object>`** en Java. Los tipos genéricos son **invariantes**, ya que permitir dicha relación rompería la seguridad de tipos. En cambio, **los arrays sí son covariantes**, por lo que `String[]` es subtipo de `Object[]`.

La covarianza de arrays provoca posibles errores en tiempo de ejecución, como intentar insertar un `Integer` en un `String[]` a través de una referencia `Object[]`, lo que genera una `ArrayStoreException`.

Un tipo genérico es **covariante** si conserva la relación de herencia (`? extends`), **contravariante** si la invierte (`? super`), e **invariante** si no permite ninguna relación de subtipo directa, como ocurre por defecto en Java.

***

## 13. Wildcards en Java

Un **wildcard** (`?`) representa un tipo desconocido en un genérico. Permite expresar covarianza y contravarianza de forma segura y controlada, sin perder el chequeo de tipos.

`List<? extends T>` se usa cuando se quiere leer valores de la lista sin modificarlos, garantizando que contienen subtipos de `T`. `List<? super T>` se emplea cuando se quiere escribir valores de tipo `T` en la lista.

```java
// Suma de números (covarianza)
double suma(List<? extends Number> lista) {
    double total = 0;
    for (Number n : lista) {
        total += n.doubleValue();
    }
    return total;
}

// Añadir enteros (contravarianza)
void añadirEnteros(List<? super Integer> lista) {
    lista.add(1);
    lista.add(2);
    lista.add(3);
}
```

De este modo, los wildcards permiten recuperar flexibilidad en los genéricos sin sacrificar seguridad.


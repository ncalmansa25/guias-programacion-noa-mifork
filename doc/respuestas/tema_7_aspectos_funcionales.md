

***

## 1. Punteros a funciones en C

Un **puntero a función** es una variable que almacena la dirección de una función. En C, las funciones no son objetos, pero sí se puede hacer referencia a ellas mediante punteros, lo que permite pasarlas como argumento, almacenarlas en estructuras o decidir dinámicamente qué función ejecutar.

Este mecanismo es muy habitual en C para implementar *callbacks*, simulaciones de polimorfismo o tablas de funciones. Sin embargo, el lenguaje no proporciona información adicional sobre el contexto ni el estado asociado a la función, solo permite invocarla.

```c
#include <stdio.h>
#include <ctype.h>

void aMayusculas(char *cadena) {
    for (int i = 0; cadena[i] != '\0'; i++) {
        cadena[i] = toupper(cadena[i]);
    }
}

int main() {
    char texto[] = "hola mundo";

    void (*func)(char*) = aMayusculas;
    func(texto);

    printf("%s\n", texto);
    return 0;
}
```

***

## 2. Funciones lambda

Una **función lambda** es una función anónima que puede definirse de forma literal y asignarse a una variable o pasarse como argumento. Permite expresar comportamientos de forma concisa, sin necesidad de definir funciones con nombre explícito.

En JavaScript, las funciones son ciudadanos de primera clase desde su origen. En Java, las lambdas se incorporaron a partir de Java 8, asociándose a interfaces funcionales para mantener el chequeo estático de tipos.

```javascript
// JavaScript
const aMayusculas = s => s.toUpperCase();
console.log(aMayusculas("hola"));
```

```java
// Java
Function<String, String> aMayusculas =
    s -> s.toUpperCase();

System.out.println(aMayusculas.apply("hola"));
```

***

## 3. Paradigma funcional y lenguajes multiparadigma

El **paradigma funcional** es un estilo de programación que modela los programas como evaluaciones de funciones, evitando el estado mutable y los efectos secundarios siempre que sea posible. Se centra en el *qué* se quiere calcular más que en el *cómo* hacerlo paso a paso.

Lenguajes como Java se califican como **multiparadigma** porque, aunque fueron diseñados principalmente bajo el paradigma orientado a objetos, incorporan características funcionales como lambdas, funciones de orden superior y programación declarativa con *streams*.

Decir que las funciones son **ciudadanos de primera clase** significa que pueden almacenarse en variables, pasarse como argumentos y devolverse como resultados, de la misma forma que cualquier otro valor del lenguaje.

***

## 4. Sintaxis básica de una lambda en Java

La sintaxis básica de una función lambda en Java se compone de tres partes: los parámetros, el operador `->` y el cuerpo de la función. Los parámetros pueden ir entre paréntesis y su tipo puede omitirse si el compilador puede inferirlo.

El cuerpo puede ser una única expresión o un bloque de instrucciones. En el primer caso, el valor de la expresión se devuelve implícitamente; en el segundo, debe usarse `return`.

```java
x -> x * 2
(x, y) -> x + y
(String s) -> { return s.toUpperCase(); }
```

Las lambdas siempre se asignan a un tipo que sea una interfaz funcional, nunca existen de forma aislada.

***

## 5. Recibir funciones como parámetros

Una característica esencial de la programación funcional es la posibilidad de **pasar funciones como argumentos**. Esto permite escribir código más reutilizable, delegando el comportamiento concreto en la función recibida.

Tanto en JavaScript como en Java, un método puede recibir una función transformadora y ejecutarla internamente sobre los datos.

```javascript
function transformar(texto, transformacion) {
    return transformacion(texto);
}
```

```java
static String transformar(String texto, Function<String, String> f) {
    return f.apply(texto);
}
```

***

## 6. Pasar lambdas directamente

Las lambdas no necesitan almacenarse previamente en una variable. Pueden definirse directamente en el punto donde se pasan como argumento, lo que mejora la expresividad y reduce código accesorio.

Esto resulta especialmente útil para comportamientos puntuales que no se reutilizan en otros lugares del programa.

```java
String resultado = transformar(
    "hola",
    s -> new StringBuilder(s).reverse().toString()
);
```

***

## 7. Cierres o *closures*

Un **closure** se produce cuando una función lambda accede a variables definidas en su contexto externo. La lambda “recuerda” el valor de esas variables incluso cuando se ejecuta fuera de su ámbito original.

En Java, las variables externas usadas en una lambda deben ser **efectivamente finales**, lo que garantiza coherencia y evita problemas de concurrencia o estado inconsistente.

```java
String sufijo = "!!!";

Function<String, String> transformar =
    s -> s + sufijo;

System.out.println(transformar.apply("Hola"));
```

***

## 8. Diferencia entre lambdas y punteros a función en C

Aunque ambos mecanismos permiten referirse a funciones, existen diferencias fundamentales. Un puntero a función en C solo apunta a código, sin capturar contexto ni estado adicional.

Las funciones lambda, en cambio, pueden capturar variables del entorno (closures), están tipadas mediante interfaces funcionales y se integran con el sistema de tipos del lenguaje. Además, permiten una sintaxis más expresiva y segura.

Por tanto, las lambdas no son solo “punteros a funciones”, sino una abstracción de nivel más alto.

***

## 9. Devolver funciones y closures

Devolver funciones permite crear **fábricas de comportamiento**, donde una función genera otras funciones especializadas. En este caso, se crea una función que devuelve otra función que aplica un descuento fijo.

```java
static Function<Double, Double> crearDescuento(double porcentaje) {
    return precio -> precio * (1 - porcentaje);
}

Function<Double, Double> d10 = crearDescuento(0.10);
Function<Double, Double> d20 = crearDescuento(0.20);

System.out.println(d10.apply(100.0)); // 90.0
System.out.println(d20.apply(100.0)); // 80.0
```

La función descuento es un closure, ya que captura el valor de `porcentaje`, que permanece disponible incluso después de que `crearDescuento` haya terminado su ejecución.

***

## 10. Interfaces funcionales

Una **interfaz funcional** es una interfaz que declara **exactamente un método abstracto**. Es el tipo al que se asignan las funciones lambda en Java.

Puede contener métodos `default` o `static`, pero solo un método abstracto. Esta restricción permite al compilador saber qué método implementar al usar una lambda.

Ejemplos típicos son `Runnable`, `Comparator` o `Function<T, R>`.

***

## 11. Interfaz funcional `Transformador`

Se puede definir una interfaz funcional personalizada para transformar cadenas de texto, manteniendo claridad semántica y reutilización.

```java
@FunctionalInterface
interface Transformador {
    String transformar(String s);
}
```

Esta interfaz puede utilizarse exactamente igual que `Function<String, String>`, pero con un nombre más expresivo en determinados contextos.

***

## 12. Interfaz funcional genérica

Generalizando la interfaz anterior mediante *generics*, se puede definir un transformador entre cualquier par de tipos.

```java
@FunctionalInterface
interface Transformador<T, R> {
    R transformar(T valor);
}

Transformador<Double, Integer> redondear =
    d -> (int) Math.round(d);
```

Este diseño incrementa notablemente la reutilización sin perder el chequeo estático de tipos.

***

## 13. Interfaces funcionales predefinidas en Java

Java proporciona un amplio conjunto de interfaces funcionales en `java.util.function`. Algunas de las más importantes son:

*   `Function<T, R>`
*   `Consumer<T>`
*   `Supplier<T>`
*   `Predicate<T>`
*   `UnaryOperator<T>`
*   `BinaryOperator<T>`

Estas interfaces cubren la mayoría de los patrones funcionales habituales y evitan la necesidad de definir interfaces propias en muchos casos.

***

## 14. `forEach` como alternativa funcional al `for`

El método `forEach` permite recorrer colecciones aplicando una función a cada elemento, sustituyendo bucles explícitos por un estilo declarativo.

```java
list.forEach(i -> {
    if (i > 0) {
        System.out.println("Positivo: " + i);
    }
});
```

Este enfoque mejora la legibilidad y encaja de forma natural con lambdas y referencias a métodos.

***

## 15. PECS y `Consumer<? super T>`

PECS significa **Producer Extends, Consumer Super**. Se utiliza para decidir si un genérico debe declararse con `extends` o `super`.

`forEach` usa `Consumer<? super T>` porque el consumidor recibe (consume) elementos de tipo `T` o de sus supertipos. Esto permite mayor flexibilidad sin comprometer la seguridad de tipos.

El mismo criterio puede aplicarse al método `transformar`, permitiendo aceptar funciones que produzcan o consuman subtipos de forma segura.

***

## 16. Referencias a métodos

Las referencias a métodos permiten reutilizar métodos existentes sin definir una lambda explícita. Capturan un método y lo tratan como una función.

```javascript
class Persona {
    constructor(nombre) {
        this.nombre = nombre;
    }
    saludar() {
        console.log("Hola, soy " + this.nombre);
    }
}

const p = new Persona("Ana");
const saludo = p.saludar.bind(p);
saludo();
```

```java
class Persona {
    private final String nombre;
    Persona(String n) { nombre = n; }
    void saludar() {
        System.out.println("Hola, soy " + nombre);
    }
}

Persona p = new Persona("Ana");
Runnable r = p::saludar;
r.run();
```

***

## 17. Tipos de referencias a método en Java

Java permite cuatro tipos principales de referencias a método:

```java
// Método estático
Math::abs

// Constructor
Persona::new

// Método de una instancia concreta
p::saludar

// Método de instancia de cualquier objeto
String::toUpperCase
```

Estas referencias mejoran la legibilidad cuando una lambda simplemente delega en un método existente.

***

## 18. Ordenación funcional con `Comparator`

Primero, una comparación implementada manualmente:

```java
Collections.sort(personas, (p1, p2) -> {
    int cmp = Integer.compare(p1.getEdad(), p2.getEdad());
    if (cmp != 0) return cmp;
    return p1.getNombre().compareTo(p2.getNombre());
});
```

Y ahora usando utilidades de `Comparator`:

```java
Collections.sort(
    personas,
    Comparator.comparing(Persona::getEdad)
              .thenComparing(Persona::getNombre)
);
```

La segunda versión es más declarativa, legible y reutiliza componentes estándar del lenguaje, ilustrando claramente las ventajas del enfoque funcional en Java.

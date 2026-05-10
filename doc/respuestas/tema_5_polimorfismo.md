***

## 1. ¿Qué es el polimorfismo y qué es la sobreescritura?

El **polimorfismo** es uno de los pilares de la programación orientada a objetos y permite que una misma referencia pueda apuntar a objetos de distintas clases relacionadas por herencia, comportándose de forma diferente según el objeto concreto al que apunte. Dicho de otro modo, posibilita que se invoque el mismo método sobre objetos distintos y que cada uno ejecute su propia versión del comportamiento. Esto favorece la flexibilidad del código y reduce la dependencia entre partes del programa.

El polimorfismo resulta especialmente útil cuando se trabaja con jerarquías de clases, ya que permite programar contra tipos generales (clases base o interfaces) sin conocer el tipo concreto en tiempo de compilación. De esta forma, se pueden añadir nuevas subclases sin modificar el código que ya utiliza la clase base, lo que mejora la extensibilidad y el mantenimiento del software.

La **sobreescritura de métodos** ocurre cuando una subclase proporciona su propia implementación de un método que ya existe en la clase base, manteniendo la misma firma (nombre y parámetros). Gracias a la sobreescritura, cada subclase puede definir un comportamiento específico para un mismo mensaje, y es el mecanismo que hace posible el polimorfismo en tiempo de ejecución.

***

## 2. Ligadura dinámica y relación con el polimorfismo

La **ligadura dinámica** (o enlace tardío) es el mecanismo mediante el cual se decide qué versión de un método se ejecuta en tiempo de ejecución y no en tiempo de compilación. Esto implica que la decisión depende del tipo real del objeto al que apunta la referencia, y no del tipo de la referencia en sí. Es un concepto clave para que el polimorfismo funcione correctamente.

La relación entre ligadura dinámica y polimorfismo es directa: sin ligadura dinámica, llamar a un método mediante una referencia de la clase base siempre ejecutaría la versión de la clase base. Gracias al enlace tardío, si el objeto real es de una subclase, se ejecuta el método sobreescrito correspondiente, logrando el comportamiento polimórfico.

En **C++**, la ligadura dinámica solo se activa si el método se declara como `virtual`. En caso contrario, el enlace es estático. En **Java**, en cambio, todos los métodos no `static`, no `final` y no `private` usan ligadura dinámica por defecto, sin necesidad de indicarlo explícitamente. **Python** va aún más allá, ya que todo se resuelve dinámicamente y el polimorfismo se basa en el modelo de tipado dinámico y el concepto de *duck typing*.

***

## 3. Ejemplo sencillo de polimorfismo en Java

En este ejemplo se define una clase base `Soldado` con un método `saluda`. A partir de ella se crean dos subclases, `Zapador` y `Artillero`. La clase `Zapador` sobreescribe completamente el método `saluda`, proporcionando un comportamiento distinto al del soldado genérico.

```java
class Soldado {
    public void saluda() {
        System.out.println("Soldado: ¡Saludos!");
    }
}

class Zapador extends Soldado {
    @Override
    public void saluda() {
        System.out.println("Zapador: ¡Saludos especializados!");
    }
}

class Artillero extends Soldado {
    // Usa el saludo por defecto
}
```

Para ilustrar el polimorfismo, se crea un array de `Soldado` que contiene objetos de distintos tipos. Aunque las referencias son de tipo `Soldado`, al invocar `saluda` se ejecuta la versión correspondiente al tipo real del objeto.

```java
Soldado[] ejercito = {
    new Soldado(),
    new Zapador(),
    new Artillero()
};

for (Soldado s : ejercito) {
    s.saluda();
}
```

Esto demuestra cómo una misma llamada a método produce comportamientos distintos gracias al polimorfismo.

***

## 4. Invocar el método base desde una sobreescritura

Al sobreescribir un método en una subclase, es posible invocar la implementación de la clase base para reutilizar parte de su comportamiento y ampliarlo. Esto resulta útil cuando solo se desea modificar o extender ligeramente el funcionamiento original, en lugar de reemplazarlo por completo.

En Java, para acceder al método de la clase base se utiliza la palabra clave `super`. Esta palabra permite llamar explícitamente al método original antes o después de añadir el nuevo comportamiento definido en la subclase.

```java
class Zapador extends Soldado {
    @Override
    public void saluda() {
        super.saluda();
        System.out.println("ZAPADOR A SUS ÓRDENES");
    }
}
```

En este caso, el zapador saluda como un soldado normal y, además, añade su mensaje particular. La palabra clave utilizada para invocar el método base es `super`.

***

## 5. Restricciones en la sobreescritura y diferencia con la sobrecarga

Al sobreescribir un método en Java, los tipos de los parámetros deben coincidir exactamente con los del método original. El tipo de retorno también debe ser el mismo, aunque se permite un retorno covariante, es decir, un subtipo del tipo de retorno original. Además, no se puede reducir la visibilidad del método (por ejemplo, pasar de `public` a `protected`).

La **sobreescritura (overriding)** ocurre entre una clase base y una subclase, y está relacionada con el polimorfismo en tiempo de ejecución. La **sobrecarga (overloading)** consiste en definir varios métodos con el mismo nombre pero distinta lista de parámetros dentro de una misma clase, y se resuelve en tiempo de compilación, sin relación directa con el polimorfismo.

La anotación `@Override` indica explícitamente que un método pretende sobreescribir otro de la clase base. Su uso es altamente recomendable, ya que el compilador puede detectar errores como firmas incorrectas o métodos que no coinciden realmente con ninguno heredado, evitando fallos sutiles en el comportamiento polimórfico.

***

## 6. Uso temprano del polimorfismo en Java

En Java, el polimorfismo se emplea desde los primeros temas, aunque no siempre se identifique explícitamente como tal. Al sobreescribir métodos como `toString` o `equals`, ya se está utilizando polimorfismo, dado que estos métodos están definidos en la clase `Object` y se redefinen en clases concretas.

Cuando se invoca `toString` sobre una referencia de tipo `Object`, el método que se ejecuta depende del tipo real del objeto. Esto es un ejemplo claro de enlace tardío y comportamiento polimórfico, incluso si el programador principiante no es plenamente consciente de ello.

Por tanto, puede afirmarse que Java introduce el polimorfismo de forma progresiva y natural. A medida que se comprende la herencia y la sobreescritura, se va tomando conciencia de que ya se estaba usando polimorfismo en ejemplos cotidianos del lenguaje.

***

## 7. Clases y métodos abstractos

Una **clase abstracta** es una clase que no puede instanciarse directamente y que está pensada para servir como base de otras clases. Puede contener métodos concretos y métodos abstractos, así como atributos y constructores.

Un **método abstracto** es un método que no tiene implementación y obliga a las subclases a proporcionar una definición concreta. Una clase que contenga al menos un método abstracto debe ser declarada como abstracta. No es posible crear instancias de una clase abstracta.

```java
abstract class Soldado {
    public void saluda() {
        System.out.println("Soldado: saludo estándar");
    }

    public abstract void atacar();
}

class Zapador extends Soldado {
    @Override
    public void atacar() {
        System.out.println("El zapador coloca explosivos");
    }
}

class Artillero extends Soldado {
    @Override
    public void atacar() {
        System.out.println("El artillero dispara el cañón");
    }
}
```

La palabra clave `abstract` debe colocarse tanto en la declaración de la clase como en la firma del método abstracto.

***

## 8. Uso de `final` y relación con el polimorfismo

La palabra clave `final` en Java impide la modificación posterior de un elemento. Si se aplica a un **método**, este no puede ser sobreescrito en las subclases. Si se aplica a una **clase**, esta no puede ser heredada.

Dado que el polimorfismo se basa en la herencia y en la sobreescritura de métodos, el uso de `final` limita directamente el polimorfismo. Un método `final` siempre ejecutará la versión definida en la clase donde se declara, independientemente del tipo real del objeto.

Un ejemplo clásico de clase `final` en la API estándar de Java es `String`. Esta decisión garantiza la inmutabilidad y seguridad del tipo, pero impide cualquier forma de extensión o comportamiento polimórfico basado en herencia.

***

## 9. Interfaces en Java

Una **interfaz** en Java define un conjunto de métodos que una clase se compromete a implementar. A diferencia de las clases abstractas, una interfaz no representa una jerarquía “es-un”, sino un contrato de comportamiento que múltiples clases pueden cumplir, incluso aunque no estén relacionadas entre sí.

Las interfaces pueden verse como una forma más pura de abstracción. Tradicionalmente solo contenían métodos abstractos (aunque hoy en día también pueden incluir métodos `default` y `static`). No poseen estado, salvo constantes implícitas.

Una clase puede **implementar más de una interfaz**, lo que permite una forma de herencia múltiple de comportamiento abstracto. Esto soluciona una de las limitaciones de Java, que no permite herencia múltiple de clases, y es una herramienta fundamental para diseñar sistemas flexibles y polimórficos.

***

## 10. Ejemplo de polimorfismo con puntos 2D y 3D

Se define una clase abstracta `Punto` con un método abstracto `calcularDistanciaA`. Las subclases `Punto2D` y `Punto3D` implementan el cálculo correspondiente. El método verifica que el punto recibido sea del mismo tipo usando `instanceof` y realiza *downcasting* para acceder a los datos necesarios.

```java
abstract class Punto {
    public abstract double calcularDistanciaA(Punto otro);
}

class Punto2D extends Punto {
    double x, y;

    @Override
    public double calcularDistanciaA(Punto otro) {
        if (otro instanceof Punto2D) {
            Punto2D p = (Punto2D) otro;
            return Math.sqrt(Math.pow(x - p.x, 2) + Math.pow(y - p.y, 2));
        }
        throw new IllegalArgumentException("Punto incompatible");
    }
}

class Punto3D extends Punto {
    double x, y, z;

    @Override
    public double calcularDistanciaA(Punto otro) {
        if (otro instanceof Punto3D) {
            Punto3D p = (Punto3D) otro;
            return Math.sqrt(
                Math.pow(x - p.x, 2) +
                Math.pow(y - p.y, 2) +
                Math.pow(z - p.z, 2)
            );
        }
        throw new IllegalArgumentException("Punto incompatible");
    }
}
```

La clase `Linea` acepta referencias de tipo `Punto` sin conocer su dimensión concreta. Gracias al polimorfismo, puede calcular su longitud invocando el método abstracto, que se resuelve dinámicamente según el tipo real de los puntos.

***

## 11. Herencia de interfaces en Java

La **herencia de interfaces** consiste en que una interfaz puede extender a otra, heredando sus métodos y añadiendo nuevos. Java permite **herencia múltiple de interfaces**, es decir, una interfaz puede extender varias interfaces a la vez, y una clase puede implementar varias interfaces simultáneamente.

Este mecanismo permite construir contratos de comportamiento complejos de forma modular. Las interfaces hijas amplían las capacidades definidas por las interfaces base, manteniendo una clara separación de responsabilidades.

```java
interface Fichero {
    String leer();
}

interface FicheroEscribible extends Fichero {
    void escribir(String contenido);
    void eliminar();
}
```

Cualquier clase que implemente `FicheroEscribible` estará obligada a proporcionar implementación tanto para los métodos heredados de `Fichero` como para los nuevos, beneficiándose de un diseño flexible y claramente polimórfico.


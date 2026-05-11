<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Genericidad". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: clases y objetos, encapsulación, excepciones, composición, herencia y polimorfismo.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 6. Genericidad

## 1. Empleando `void*` en C o `Object` en Java, pon un ejemplo de una estructura de datos, que empleando un array primitivo, permita alojar cualquier tipo de dato.

### Respuesta

En lenguajes sin mecanismos avanzados de genericidad, como C o Java sin generics, una forma clásica de simular estructuras de datos genéricas consiste en almacenar referencias a un tipo base común. En C, ese tipo es void*, que representa un puntero a memoria sin tipo concreto. En Java, el papel equivalente lo desempeña la clase Object, superclase de todas las clases.
Este enfoque permite crear estructuras de datos, como arrays o listas, capaces de almacenar “cualquier cosa”, ya que cualquier puntero en C puede convertirse a void*, y cualquier objeto en Java es un Object. Sin embargo, esta flexibilidad se obtiene a costa de perder información de tipo, que deberá recuperarse más adelante mediante conversiones explícitas.

// C con void*
void* array[10];
array[0] = malloc(sizeof(int));
*(int*)array[0] = 5;

// Java con Object
Object[] array = new Object[10];
array[0] = "Hola";
array[1] = 42; // Integer

## 2. Brevemente, ¿Qué significa la **programación genérica**? ¿Es el ejemplo anterior un ejemplo básico de programación genérica? 

### Respuesta

La programación genérica es un paradigma que permite escribir algoritmos y estructuras de datos independientes de los tipos concretos con los que operan, manteniendo al mismo tiempo el chequeo de tipos en tiempo de compilación. El objetivo es reutilizar código sin renunciar a la seguridad de tipos.
El ejemplo basado en void* o Object puede considerarse una forma muy básica de programación genérica, pero incompleta. Aunque permite trabajar con distintos tipos, no proporciona garantías de corrección en tiempo de compilación. La genericidad “real” empieza cuando el lenguaje es capaz de verificar automáticamente que los tipos usados son coherentes.


## 3. Indica los problemas respecto al chequeo de tipos, de emplear `void*` o `Object` cuando se crean estructuras de datos genéricas. 

### Respuesta

El principal problema de emplear void* en C o Object en Java es la pérdida de chequeo de tipos en tiempo de compilación. El compilador ya no puede asegurar que los elementos extraídos de la estructura sean del tipo correcto, lo que obliga a realizar conversiones explícitas (casting).
Estas conversiones pueden ser erróneas y provocar fallos en tiempo de ejecución, como segmentation faults en C o ClassCastException en Java. Además, el código se vuelve más difícil de leer, mantener y refactorizar, ya que la información de tipo queda dispersa y no explícita.

## 4. Vamos entonces con mecanismos de mejora de la programación genérica ¿Qué son los **parámetros de tipo**? 

### Respuesta

Los parámetros de tipo son marcadores que representan tipos desconocidos y se especifican al definir una clase, interfaz o método genérico. Se suelen escribir entre signos < >, como <T>, y permiten que el compilador razone sobre los tipos concretos que se usarán más adelante.
Gracias a los parámetros de tipo, el código genérico conserva toda la información de tipos necesaria para garantizar que las operaciones realizadas son seguras, evitando casts innecesarios y errores en tiempo de ejecución. Este mecanismo es la base de los generics en Java y los templates en C++.

## 5. En Java existe "generics", en C++ existen "templates". Pon un ejemplo de uso de programación genérica en ambos, instanciando una lista o vector dinámico que solo admite `String`. Introduce valores, y luego haz un recorrido de ellos mostrando cómo cada elemento es del tipo concreto con seguridad.

### Respuesta

En Java, los generics permiten parametrizar clases como List<T>. Al instanciarlas con un tipo concreto, por ejemplo String, el compilador garantiza que solo se almacenarán y recuperarán objetos de ese tipo.

List<String> lista = new ArrayList<>();
lista.add("uno");
lista.add("dos");

for (String s : lista) {
    System.out.println(s.toUpperCase());
}
``
En C++, los templates funcionan de forma similar, aunque con un mecanismo distinto a nivel de compilación.

#include <vector>
#include <string>

std::vector<std::string> v;
v.push_back("uno");
v.push_back("dos");

for (const std::string& s : v) {
    std::cout << s << std::endl;
}
``

## 6. Sobre el funcionamiento de la programación genérica. ¿Qué hace el compilador cuando se instancia una clase que tiene parámetros de tipo? ¿Hace lo mismo C++ y Java? ¿Qué es el "type erasure" de Java y la "instanciación de plantillas" de C++?

### Respuesta

Cuando se instancia una clase genérica, el compilador trata el parámetro de tipo de forma distinta según el lenguaje. En Java, se aplica el mecanismo de type erasure: la información de los parámetros de tipo se elimina tras la compilación y se sustituye por Object o por su límite superior (bound).
En C++, ocurre lo contrario. Cada uso de un template con tipos concretos genera una instanciación de plantilla independiente, produciendo código específico para cada combinación de tipos. Esto aumenta el tamaño del binario pero conserva la información de tipo exacta.
Por tanto, Java favorece compatibilidad y simplicidad en la máquina virtual, mientras que C++ prioriza rendimiento y especialización del código.


## 7. Vamos a crear una nueva clase con parámetros de tipo. Define en Java una clase `Par`, que permite alojar dos valores de tipos diferentes. Incluye un constructor y un getter para cada tipo. Pon un ejemplo de uso de ese `Par`, por ejemplo para especificar el tipo de retorno de una función que devuelve en un `Par` la media y desviación típica de un array de `double`. 

### Respuesta

Se puede definir una clase genérica con dos parámetros de tipo para almacenar dos valores de tipos distintos. Esto permite expresar de forma clara relaciones entre datos heterogéneos.

public class Par<A, B> {
    private A primero;
    private B segundo;

    public Par(A primero, B segundo) {
        this.primero = primero;
        this.segundo = segundo;
    }

    public A getPrimero() { return primero; }
    public B getSegundo() { return segundo; }
}

public static Par<Double, Double> calcularMediaYDesviacion(double[] datos) {
    // cálculo omitido
    return new Par<>(media, desviacion);
}

Este diseño evita crear clases específicas solo para empaquetar resultados.

## 8. En Java, se pueden declarar parámetros de tipo también a nivel de método, no solo a nivel de clase. Pon un ejemplo con un método genérico `seleccionaUno`, que pasados dos objetos del mismo tipo, te devuelva aleatoriamente uno de ellos. Muestra la diferencia de definirlo con dos `Object`, a definirlo con dos parámetros de tipo, en terminos de (i) evitar downcasting y (ii) forzar que ambos objetos sean del mismo tipo. 

### Respuesta

En Java, los parámetros de tipo pueden declararse también a nivel de método. Un método genérico permite inferir el tipo automáticamente y mantener coherencia entre los parámetros y el valor devuelto.

public static <T> T seleccionaUno(T a, T b) {
    return Math.random() < 0.5 ? a : b;
}
Si se usara Object, sería necesario un downcasting al recuperar el valor y no se forzaría que ambos argumentos fueran del mismo tipo. Con genéricos, el compilador garantiza ambas propiedades de forma automática.

## 9. ¿Se pueden establecer restricciones en los parámetros de tipo? Por ejemplo, si quiero definir un tipo genérico `<T>`, ¿puedo decir que tenga que ser, al menos, un número para poder tratarlo como tal? Pon un ejemplo en Java de un `Punto` con dos coordenadas, metodos `getX`, `getY`, y una función `calcularDistanciaA` otro `Punto`. Permite que esas coordenadas sean cualquier tipo de número. Pon dos soluciones: una simplemente creando coordenadas de tipo `Number` y otra añadiendo generics para reforzar el chequeo de tipos y saber exactamente con qué tipo de número trabaja el `Punto`. En este caso y respecto al "type erasure", ¿cuál es el tipo final tras la compilación?

### Respuesta

En Java es posible restringir los parámetros de tipo mediante bounds, por ejemplo <T extends Number>. Sin genéricos, se puede usar directamente Number como tipo de las coordenadas.

class PuntoSimple {
    private Number x, y;
}
``
class PuntoSimple {
    private Number x, y;
}
``
class Punto<T extends Number> {
    private T x, y;
}

Debido al type erasure, tras la compilación el tipo real será Number, aunque en el código fuente se mantenga la información genérica.

## 10. Sobre las soluciones anteriores. Si bien ambas permiten trabajar con distintos tipos de número sin duplicar la clase `Punto`, reflexiona sobre el refuerzo del chequeo de tipos con generics. ¿Permiten ambas crear un punto con una coordenada de tipo entero y la otra coordenada de tipo real? ¿Qué tipo devuelve el `getX` con la solucion sin generics y qué tipo devuelve el que tiene la solución con generics?

### Respuesta

Ambas soluciones permiten reutilizar la clase Punto para distintos tipos numéricos, pero solo la versión genérica refuerza el chequeo de tipos en tiempo de compilación. En la versión sin genéricos, es posible combinar un Integer y un Double sin advertencia.
En cuanto a los métodos, getX() devuelve Number en la versión sin genéricos, mientras que en la versión genérica devuelve exactamente T, lo que preserva información de tipo y evita conversiones innecesarias.

## 11. Hagamos un ejemplo avanzado. El siguiente código, con interfaz `Punto`, que define un método `calcularDistanciaA(Punto p)`, junto con las implementaciones `Punto2D` y `Punto3D`. Añade generics para asegurarnos que la sobreescritura del método calcular distancia a otro `Punto` siempre es sobre un `Punto` del mismo tipo, evitando `instanceof` y el downcasting.
```java
public interface Punto { 
    public double distanciaA(Punto p); 
} 

public class Punto2D implements Punto { 
     private final double x, y; 
     public Punto2D(double x, double y) { 
        this.x = x; this.y = y; 
    } 

    @Override 
    public double distanciaA(Punto p) { 
        if (p instanceof Punto2D) { 
            Punto2D p2d = (Punto2D) p; 
            return Math.sqrt(Math.pow(x - p2d.x, 2) 
                    + Math.pow(y - p2d.y, 2)); 
        } else { 
            throw new RuntimeException("p debe ser Punto 2D"); 
        } 
    } 
} 
public class Punto3D implements Punto { 
    // Igual que Punto2D, pero con tres coordenadas
    ...
} 
```

### Respuesta

Se puede parametrizar la interfaz para asegurar que la distancia se calcula siempre entre puntos del mismo tipo concreto.

public interface Punto<T extends Punto<T>> {
    double distanciaA(T p);
}
``

public class Punto2D implements Punto<Punto2D> {
    @Override
    public double distanciaA(Punto2D p) {
        ...
    }
}

Este patrón evita el uso de instanceof y downcasting, reforzando el polimorfismo con chequeo estático.

## 12. Dado que `String` es subtipo de `Object`, ¿significa eso que `List<String>` es subtipo de `List<Object>`? ¿Y que `String[]` es subtipo de `Object[]`? Razona por qué la respuesta es diferente en cada caso y qué problema en tiempo de ejecución puede aparecer con los arrays. A partir de estos ejemplos, define qué significa que un tipo genérico sea **covariante**, **contravariante** o **invariante** respecto a su parámetro de tipo.

### Respuesta

Aunque String sea subtipo de Object, List<String> no es subtipo de List<Object> porque los genéricos en Java son invariantes. Sin embargo, String[] sí es subtipo de Object[], lo que puede provocar errores en tiempo de ejecución como ArrayStoreException.
Un tipo es covariante si preserva la relación de herencia, contravariante si la invierte, e invariante si no admite ninguna de las dos. Los genéricos en Java son invariantes por defecto para evitar errores.

## 13. Java permite recuperar covarianza y contravarianza en tipos genéricos de forma controlada mediante **wildcards**. ¿Qué es un wildcard (`?`)? Muestra la diferencia entre `List<? extends T>` y `List<? super T>`, indicando en qué casos se usa cada uno. Pon dos ejemplos: (i) un método que reciba una lista de números y calcule su suma, usando `? extends`; (ii) un método que reciba una lista y le añada varios números enteros, usando `? super`.

### Respuesta

Un wildcard (?) representa un tipo desconocido. ? extends T permite leer valores de tipo T o subtipos, mientras que ? super T permite escribir valores de tipo T.

// ? extends
static double sumar(List<? extends Number> l) {
    ...
}

// ? super
static void añadirEnteros(List<? super Integer> l) {
    l.add(1);
    l.add(2);
}

La regla práctica es “producer extends, consumer super”: usar extends cuando se consume información y super cuando se produce.

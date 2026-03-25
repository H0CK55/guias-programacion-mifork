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


## 1. En C, podemos crear estructuras mayores **componiendo** unas con otras, que suelen describirse como "A tiene-un/tiene-varios B". Pon un ejemplo, empleando `struct`, de una línea de puntos, donde puntos tienen dos coordenadas (`x` e `y`), y la línea esta hecha de dos puntos. Incluye una función para calcular la distancia entre puntos y otra para hallar la longitud de una línea.

### Respuesta

```c
#include <stdio.h>
#include <math.h>

typedef struct {
    double x;
    double y;
} Punto;

typedef struct {
    Punto inicio;
    Punto fin;
} Linea;

double distanciaEntrePuntos(Punto a, Punto b) {
    double dx = b.x - a.x;
    double dy = b.y - a.y;
    return sqrt(dx * dx + dy * dy);
}

double longitudDeLinea(Linea l) {
    return distanciaEntrePuntos(l.inicio, l.fin);
}

int main() {
    Punto p1 = {0.0, 0.0};
    Punto p2 = {3.0, 4.0};
    Linea linea = {p1, p2};

    printf("Distancia entre puntos: %.2f\n", distanciaEntrePuntos(p1, p2));
    printf("Longitud de la línea: %.2f\n", longitudDeLinea(linea));

    return 0;
}
```

En este ejemplo se observa cómo la composición permite organizar la información de forma clara: un punto representa un dato simple con dos coordenadas, mientras que la línea agrupa dos puntos, formando una estructura mayor. Esta idea coincide con el modelo conceptual “A tiene-un B”, donde la línea *tiene* dos puntos. El uso de `typedef` facilita la escritura posterior del código y mejora su legibilidad.

Las funciones también muestran cómo se puede estructurar la lógica: primero se define una operación básica, la distancia entre dos puntos, y luego se reutiliza en una función de mayor nivel que calcula la longitud de una línea completa. Esta forma de dividir responsabilidades hace que el código sea más modular y más fácil de mantener.

## 2. Ahora transforma ese ejemplo a orientación a objetos con Java, para tener un primer ejemplo de **composición** en orientación a objetos. Crea una clase `Punto`, y una clase `Linea`. La clase `Punto` debe tener un método para calcular distancia a otro `Punto` y `Linea` debe tener un método para calcular su longitud. Gracias a la ocultación de información, supera a C, garantizando que los puntos sean inmutables, al igual que la línea, que una vez creada, no queremos que se modifique de qué a qué puntos va dicha línea.  

### Respuesta

```java
public final class Punto {
    private final double x;
    private final double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double distanciaA(Punto otro) {
        double dx = otro.x - this.x;
        double dy = otro.y - this.y;
        return Math.sqrt(dx * dx + dy * dy);
    }

    public double getX() { return x; }
    public double getY() { return y; }
}

public final class Linea {
    private final Punto inicio;
    private final Punto fin;

    public Linea(Punto inicio, Punto fin) {
        this.inicio = inicio;
        this.fin = fin;
    }

    public double longitud() {
        return inicio.distanciaA(fin);
    }

    public Punto getInicio() { return inicio; }
    public Punto getFin() { return fin; }
}
```

En este ejemplo se aplica la composición porque `Linea` **tiene** dos objetos `Punto`. Además, al declararse los atributos como `private final`, se garantiza que ni los puntos internos ni la propia línea podrán cambiarse tras la construcción. De este modo, se ofrece una mayor robustez que en C, donde la modificación de los campos de una estructura es libre y no existe un mecanismo automático para proteger los datos.

El método `distanciaA` encapsula el cálculo matemático de la distancia entre dos puntos, de forma similar al ejemplo en C, pero integrándolo dentro del propio concepto `Punto`, lo que aumenta la cohesión del diseño. Por su parte, el método `longitud` de `Linea` delega en la operación de los puntos, mostrando cómo la composición permite construir funcionalidad más compleja a partir de objetos más simples. Este tipo de organización modular es uno de los beneficios fundamentales de la orientación a objetos.


## 3. ¿Qué significa la **multiplicidad** en la composición? En el ejemplo anterior, ¿cuál es la multiplicidad entre `Linea` y `Punto`? Indícalo expresando la multiplicidad en ambas direcciones, de `Linea` a `Punto` y de `Punto` a `Linea`.

### Respuesta

La **multiplicidad** en composición describe cuántas instancias de una clase están vinculadas a instancias de otra clase dentro de una relación “tiene‑un”. Este concepto se utiliza habitualmente en diagramas UML para indicar si una clase contiene exactamente un objeto de otra clase, varios, o incluso un número variable dentro de un rango. La multiplicidad permite entender la estructura interna de las clases y las restricciones que impone el diseño, especialmente cuando se trabaja con objetos compuestos.

En el ejemplo anterior, la clase `Linea` está formada exactamente por **dos** objetos de tipo `Punto`. Esto implica que, desde la perspectiva de `Linea` hacia `Punto`, la multiplicidad es **2**, es decir, *una línea tiene exactamente dos puntos*. No se admiten ni más ni menos, ya que la estructura está diseñada para representar un segmento determinado por dos extremos bien definidos.

En dirección inversa, un `Punto` no mantiene ninguna referencia interna hacia una `Linea`, por lo que, desde el punto de vista del código, su multiplicidad hacia `Linea` es **0**. Sin embargo, si se habla del modelo conceptual, un mismo `Punto` podría ser usado como extremo en múltiples líneas distintas, por lo que la multiplicidad conceptual sería **0..**\* (un punto puede no pertenecer a ninguna línea o puede pertenecer a varias). Este matiz refleja la diferencia entre la composición explícita en el código y la posible reutilización de objetos en el programa.

Por tanto, expresadas formalmente, las multiplicidades son:

*   **De `Linea` a `Punto`: 2** (una línea tiene exactamente dos puntos).
*   **De `Punto` a `Linea`: 0..**\* en el modelo conceptual, pero **0** en el diseño concreto implementado, ya que `Punto` no conoce a las líneas que lo utilizan.


## 4. ¿Qué significa composición **fuerte** y composición **débil**? ¿Qué consecuencia implica en relación al ciclo de vida de los objetos? Indica a cuál solemos referirnos como **"asociación o agregación"** y a cuál como **"composición"** propiamente.

### Respuesta

La **composición fuerte** se refiere a una relación en la que un objeto “contenedor” es el propietario exclusivo de los objetos que contiene. Esto significa que los objetos internos no tienen un ciclo de vida independiente: existen únicamente mientras existe el objeto que los compone. Cuando el objeto contenedor es destruido o deja de existir, todos sus componentes desaparecen con él. Esta forma de composición expresa una dependencia total y suele usarse para indicar una relación estructural muy estrecha.

Por el contrario, la **composición débil** describe una relación en la que el objeto contenedor *no es dueño* de los objetos que utiliza. En este caso, los objetos internos pueden seguir existiendo aunque el objeto que los referenciaba desaparezca, lo que significa que sus ciclos de vida son independientes. Aunque existe una relación “tiene‑un”, esta es más flexible y no implica propiedad ni destrucción conjunta, lo que permite compartir objetos entre diferentes estructuras sin perder consistencia.

En terminología habitual, la composición débil suele denominarse **asociación** o **agregación**, resaltando que el vínculo entre objetos es más laxo y no implica dependencia vital. Por otro lado, la composición fuerte es la que se conoce como **composición** propiamente dicha en orientación a objetos, recalcando la idea de que el objeto compuesto engloba y controla completamente a los objetos que forman parte de él.

En el diseño de software orientado a objetos, distinguir entre ambas es esencial para modelar correctamente el ciclo de vida de los datos. La elección entre una u otra afecta tanto a la responsabilidad de creación y destrucción como a la claridad conceptual del modelo, por lo que se recomienda optar por composición fuerte solo cuando la dependencia entre objetos sea verdaderamente estructural.

## 5. Cuando una clase usa a otra al recibirla o devolverla como parámetro en algún método, al hacer `new` dentro de un método, o al usarlas como variables locales, ¿hablamos de composición o de **"dependencia"**?

### Respuesta

Cuando una clase utiliza a otra únicamente **como parámetro**, **como valor de retorno**, **como variable local** o incluso creando objetos con `new` dentro de un método, no se considera que exista composición. En estos casos se habla de **dependencia**, porque la clase solo necesita a la otra para realizar una operación puntual, sin conservarla como parte de su estructura interna. La relación es temporal y se limita al ámbito del método en el que se usa.

Esta dependencia implica que la clase **no es dueña** del objeto que emplea, ni controla su ciclo de vida. El objeto puede haber sido creado fuera, puede ser compartido con otros componentes o incluso puede desaparecer antes o después sin afectar a la clase que lo utiliza. No existen atributos internos que almacenen permanentemente la referencia, por lo que no se forma parte de su estado.

En cambio, la **composición** requiere que la clase contenga objetos como parte de su estructura interna, normalmente a través de atributos privados y creados en su constructor. Esta diferencia es esencial para distinguir relaciones fuertes (composición) de relaciones operacionales o momentáneas (dependencia). En resumen, cuando una clase usa a otra de forma no estructural y sin conservarla, se está ante una **relación de dependencia**, no de composición.

## 6. En el ejemplo anterior de línea y punto, programa la relación entre `Linea` y `Punto` de dos formas. Una **como composición fuerte**, donde el ciclo de vida de los puntos está ligado al de Linea y otra **como composición débil**, donde no.

### Respuesta

***

# ✅ **1. Composición fuerte (los puntos pertenecen a la línea)**

En esta versión, la clase `Linea` **crea sus propios puntos** y no recibe objetos externos. Los puntos solo existen como parte interna de la línea, y no pueden ser compartidos con otras líneas. De esta manera, sus ciclos de vida quedan completamente ligados: si desaparece la línea, desaparecen sus puntos. Se trata de una composición en la que la propiedad es total.

Este modelo se utiliza cuando se desea que la clase posea y controle completamente sus componentes. Es adecuado cuando conceptualmente los puntos no tienen sentido fuera del objeto “línea”, o cuando se busca evitar cualquier modificación externa no deseada. Los atributos `inicio` y `fin` se pasan como coordenadas primitivas y no como objetos `Punto`.

```java
// --- Composición fuerte ---
public final class Punto {
    private final double x;
    private final double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double distanciaA(Punto otro) {
        double dx = otro.x - this.x;
        double dy = otro.y - this.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}

public final class Linea {
    private final Punto inicio;
    private final Punto fin;

    // La línea crea sus propios puntos -> composición fuerte
    public Linea(double x1, double y1, double x2, double y2) {
        this.inicio = new Punto(x1, y1);
        this.fin = new Punto(x2, y2);
    }

    public double longitud() {
        return inicio.distanciaA(fin);
    }
}
```

***

# ✅ **2. Composición débil (la línea usa puntos ajenos)**

En este caso, la clase `Linea` recibe objetos `Punto` ya existentes, lo que significa que **no es dueña** de ellos. Los puntos pueden existir antes y después de que la línea sea destruida, y pueden ser compartidos por varias líneas. Esta relación permite mayor flexibilidad, aunque no representa control sobre el ciclo de vida.

Se trata de un ejemplo típico de **agregación**, donde la clase mantiene referencias internas, pero sin responsabilidad sobre la creación o destrucción de los objetos que utiliza. Conceptualmente sigue siendo un tipo de “tiene-un”, pero sin propiedad rígida, ya que los puntos podrían ser usados por más estructuras.

```java
// --- Composición débil (agregación) ---
public final class Punto {
    private final double x;
    private final double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double distanciaA(Punto otro) {
        double dx = otro.x - this.x;
        double dy = otro.y - this.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}

public final class Linea {
    private final Punto inicio;
    private final Punto fin;

    // La línea NO crea sus puntos -> composición débil (agregación)
    public Linea(Punto a, Punto b) {
        this.inicio = a;
        this.fin = b;
    }

    public double longitud() {
        return inicio.distanciaA(fin);
    }
}
```

***

## 7. En Java, en la composición fuerte, ¿cuando el contenedor destruye los objetos? No se observa que `Linea` destruya los `Punto` explícitamente, ¿Por qué?

### Respuesta

En Java, incluso en una **composición fuerte**, el objeto contenedor no destruye explícitamente a los objetos que contiene. Esto se debe a que Java cuenta con un **recolector de basura (Garbage Collector)** que gestiona automáticamente la memoria. Por tanto, cuando una instancia de `Linea` deja de ser accesible, sus puntos internos también pasan a estar inaccesibles, y el recolector de basura se encargará de liberar la memoria cuando lo considere oportuno. No existe ninguna instrucción equivalente a `delete` en C++, por lo que el proceso de destrucción no es responsabilidad directa del programador.

En este modelo, la idea de composición fuerte se mantiene porque los objetos `Punto` están conceptualmente “ligados” a la vida de la línea: si no hay referencias externas a ellos, su ciclo de vida termina junto con el de `Linea`. Aunque Java no requiere destruir explícitamente los objetos, la relación de propiedad se expresa al hacer que la línea cree y mantenga sus propios puntos, logrando la misma intención de diseño que en lenguajes con gestión manual de memoria.

Así, el concepto de “destrucción” en Java debe entenderse como **dejar de tener referencias vivas** hacia un objeto. Una vez que no queda ninguna referencia, el objeto pasa a ser candidato para el recolector de basura. Por ello no se observa código que destruya los puntos desde `Linea`: la liberación no es explícita ni inmediata, sino automática y dependiente de cuándo el sistema determine que es necesario recuperar memoria.

En resumen, la composición fuerte no implica destrucción manual, sino **dependencia vital a nivel conceptual**: la vida de los puntos está unida a la de la línea porque no se exponen a otras partes del programa. Pero la liberación real de memoria queda en manos del mecanismo automático de gestión de memoria de Java.

## 8. Pon un ejemplo de composicion débil entre un departamento que tiene varios profesores. Implementa dos composiciones a la vez: entre el departamento y todos sus profesores y entre el departamento y su director, que es un profesor del departamento. Siempre debe haber un director en el departamento desde el inicio. Lanza excepciones si se viola la invariante. Emplea arrays primitivos de Java, estilo `Profesor[]`, con máximo 50, pero no rompas la encapsulación, no desveles que estás empleando un array, permite añadir un `Profesor` al final de la lista, y eliminar un profesor dada su posición. Da acceso a los profesores con un método para saber cuántos hay y otro para obtener un profesor por posición. El director se puede cambiar por otro profesor del departamento. Sin embargo, ten en cuenta esta invariante de clase: el director debe formar siempre parte de la lista de profesores, es decir, ten cuidado al cambiar el director o al eliminar un profesor.

### Respuesta

***

# ✅ **Código completo**

```java
public final class Profesor {
    private final String nombre;

    public Profesor(String nombre) {
        if (nombre == null || nombre.isBlank()) {
            throw new IllegalArgumentException("El nombre no puede ser vacío.");
        }
        this.nombre = nombre;
    }

    public String getNombre() {
        return nombre;
    }
}
```

***

```java
public final class Departamento {
    private final Profesor[] profesores;
    private int numProfesores;
    private Profesor director;

    public Departamento(Profesor directorInicial) {
        if (directorInicial == null)
            throw new IllegalArgumentException("Debe haber siempre un director.");

        this.profesores = new Profesor[50];
        this.profesores[0] = directorInicial;
        this.numProfesores = 1;
        this.director = directorInicial;
    }

    // --- Métodos públicos de consulta ---
    public int getNumeroProfesores() {
        return numProfesores;
    }

    public Profesor getProfesor(int posicion) {
        if (posicion < 0 || posicion >= numProfesores)
            throw new IndexOutOfBoundsException("Posición inválida.");
        return profesores[posicion];
    }

    public Profesor getDirector() {
        return director;
    }

    // --- Añadir profesor ---
    public void añadirProfesor(Profesor p) {
        if (p == null)
            throw new IllegalArgumentException("Profesor nulo.");

        if (numProfesores == profesores.length)
            throw new IllegalStateException("No caben más profesores.");

        profesores[numProfesores++] = p;
    }

    // --- Eliminar profesor ---
    public void eliminarProfesor(int posicion) {
        if (posicion < 0 || posicion >= numProfesores)
            throw new IndexOutOfBoundsException("Posición inválida.");

        Profesor aEliminar = profesores[posicion];

        // No se permite eliminar al director
        if (aEliminar == director)
            throw new IllegalStateException("No se puede eliminar al director.");

        // Compactar array
        for (int i = posicion; i < numProfesores - 1; i++) {
            profesores[i] = profesores[i + 1];
        }
        profesores[--numProfesores] = null;
    }

    // --- Cambiar director ---
    public void cambiarDirector(Profesor nuevoDirector) {
        if (nuevoDirector == null)
            throw new IllegalArgumentException("Director no puede ser nulo.");

        // Verificar que está en la lista
        boolean existe = false;
        for (int i = 0; i < numProfesores; i++) {
            if (profesores[i] == nuevoDirector) {
                existe = true;
                break;
            }
        }

        if (!existe)
            throw new IllegalStateException("El director debe ser profesor del departamento.");

        this.director = nuevoDirector;
    }
}
```

***

En este diseño se usa composición débil porque el departamento **no crea** a los profesores ni es dueño de su ciclo de vida. Los recibe desde fuera y simplemente mantiene referencias, pudiendo compartir los mismos profesores con otros contextos si fuera necesario. El contenedor tampoco destruye a los objetos; simplemente deja de referenciar a ellos, lo que permite que su ciclo de vida siga siendo independiente. Todo esto refleja una forma típica de agregación, donde los objetos participantes tienen autonomía plena.

La clase `Departamento` mantiene la lista de profesores mediante un array interno que nunca se expone. Para evitar romper la encapsulación, se proporciona acceso a los profesores únicamente mediante métodos específicos: uno para consultar el número de profesores y otro para recuperarlos por posición. Para mantener la lista dinámica, se implementan operaciones para añadir profesores al final y para eliminarlos por índice, gestionando las posiciones internamente y evitando que se desvele el uso de un array fijo.

Una parte esencial del ejercicio es la invariante de clase que exige que el director sea siempre un profesor del departamento. Para cumplirla, la construcción inicial obliga a recibir un director, que se añade automáticamente como primer profesor del array. Durante la eliminación de profesores, se impide borrar al director y, al cambiar de director, se verifica que el nuevo candidato también forme parte del departamento, reforzando así la coherencia interna del objeto. Este control de integridad garantiza que en ningún momento el estado del departamento quede inconsistente o incompleto.

El resultado final es un diseño robusto que demuestra cómo se puede modelar una composición débil sin romper la encapsulación, asegurando a la vez que ciertas reglas lógicas —como la presencia continua de un director— se mantengan siempre vivas. La gestión manual del array permite comprender cómo construir colecciones propias sin depender de estructuras dinámicas como `ArrayList`, adecuándose a las exigencias del ejercicio.

***

## 9. En Java, existen también `List`, cambia y muestra cómo sería el código anterior empleando `List` en vez de arrays primitivos. ¿Qué parte del código original te has ahorrado? Además, fíjate en el método `getProfesor(int pos)`: si en su lugar existiera un método que devolviera todos los profesores a la vez, ¿qué problema tendría devolver directamente la lista interna? ¿Cómo lo resolverías?

### Respuesta

A continuación se presenta una versión del ejercicio usando **`List<Profesor>`** en lugar de arrays primitivos. Con ello se evita gestionar manualmente el tamaño, la compactación del array tras eliminar elementos o la verificación de límites, porque `List` ya ofrece métodos como `add`, `remove` y `size`. Esto hace que el código sea más claro y menos propenso a errores, al delegar la gestión interna en la propia colección de Java.

Se mantiene la invariante de que el director debe ser siempre un profesor del departamento y de que siempre debe haber un director desde el momento de creación. Además, se explica por qué devolver la lista interna directamente rompería la encapsulación, y cómo solucionar ese problema.

***

# ✅ **Código con `List<Profesor>`**

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public final class Profesor {
    private final String nombre;

    public Profesor(String nombre) {
        if (nombre == null || nombre.isBlank()) {
            throw new IllegalArgumentException("El nombre no puede ser vacío.");
        }
        this.nombre = nombre;
    }

    public String getNombre() {
        return nombre;
    }
}
```

***

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public final class Departamento {
    private final List<Profesor> profesores;
    private Profesor director;

    public Departamento(Profesor directorInicial) {
        if (directorInicial == null)
            throw new IllegalArgumentException("Debe existir director.");

        this.profesores = new ArrayList<>();
        this.profesores.add(directorInicial);
        this.director = directorInicial;
    }

    // --- Consultas ---
    public int getNumeroProfesores() {
        return profesores.size();
    }

    public Profesor getProfesor(int pos) {
        return profesores.get(pos); // List ya verifica bounds
    }

    public Profesor getDirector() {
        return director;
    }

    // --- Añadir profesor ---
    public void añadirProfesor(Profesor p) {
        if (p == null)
            throw new IllegalArgumentException("Profesor nulo.");
        profesores.add(p);
    }

    // --- Eliminar profesor ---
    public void eliminarProfesor(int pos) {
        Profesor aEliminar = profesores.get(pos); // List gestiona el índice

        if (aEliminar == director)
            throw new IllegalStateException("No se puede eliminar al director.");

        profesores.remove(pos); 
    }

    // --- Cambiar director ---
    public void cambiarDirector(Profesor nuevoDirector) {
        if (nuevoDirector == null)
            throw new IllegalArgumentException("Director no puede ser nulo.");

        if (!profesores.contains(nuevoDirector))
            throw new IllegalStateException("El director debe formar parte del departamento.");

        this.director = nuevoDirector;
    }

    // --- Si se quisiera devolver todos los profesores ---
    public List<Profesor> getProfesores() {
        return Collections.unmodifiableList(profesores);
    }
}
```

***

# ✅ **¿Qué parte del código original se ha ahorrado?**

Al utilizar `List`, ya no es necesario gestionar manualmente el tamaño máximo, desplazar elementos tras un borrado ni comprobar explícitamente los límites del array. La colección se encarga de la gestión interna y proporciona operaciones seguras como `add`, `remove`, `size` o `contains`, lo que simplifica el código y reduce el riesgo de errores. Tampoco es necesario inicializar un array de tamaño fijo ni almacenar un contador manual, porque la lista mantiene su propio tamaño dinámico.

Gracias a esta abstracción, la lógica de la clase queda más centrada en las reglas del dominio (por ejemplo, mantener la invariante del director) y menos en detalles de infraestructura como la memoria o el desplazamiento de elementos. Esto refleja una de las ventajas principales de las colecciones frente a los arrays primitivos: mayor expresividad y menor complejidad accidental. El resultado es un código más legible y mantenible, alineado con las prácticas habituales en Java moderno.

# ✅ **¿Por qué no se puede devolver la lista interna directamente? ¿Cuál sería el problema?**

Si se devolviera directamente la lista interna (por ejemplo `return profesores;`), cualquier código externo podría modificarla libremente: añadir profesores, eliminarlos, reordenarlos o incluso eliminar accidentalmente al director. Esto rompería la encapsulación y permitiría violar las invariantes que la clase está diseñada para proteger. Dado que una lista es una estructura mutable, exponerla directamente significa perder el control sobre la consistencia interna del objeto.

La forma correcta de resolverlo es devolver una versión **inmodificable** de la lista mediante `Collections.unmodifiableList(profesores)`. Esta técnica permite ofrecer acceso de solo lectura sin permitir alteraciones externas. Otra opción sería devolver una **copia defensiva**, como `new ArrayList<>(profesores)`, lo que también protege la estructura interna a costa de un pequeño coste adicional. En ambos casos se garantiza que la invariante del objeto no pueda romperse desde fuera.

***

## 10. Al igual que ocurre con las excepciones en Java, que pueden encerrar causas (que son excepciones), de forma recursiva, suponen un tipo especial de composiciones, denominadas composiciones recursivas. Pon un ejemplo en Java de una `Persona`, que sea inmutable, y que tiene una madre, que es otra `Persona`. Haz un main con un ejemplo de uso con una familia de personas, desde el nieto hasta la abuela. Enumera algún otro ejemplo clásico de composiciones recursivas.

### Respuesta

A continuación se muestra un ejemplo completo de **composición recursiva** en Java, donde una `Persona` es inmutable y contiene a su **madre**, que es también otra `Persona`. Este tipo de composición se denomina *recursiva* porque una instancia contiene otra instancia del mismo tipo, igual que ocurre con excepciones que contienen sus causas.

***

# ✅ Código: `Persona` inmutable con composición recursiva

```java
public final class Persona {
    private final String nombre;
    private final Persona madre;

    public Persona(String nombre, Persona madre) {
        if (nombre == null || nombre.isBlank()) {
            throw new IllegalArgumentException("El nombre no puede ser vacío.");
        }
        this.nombre = nombre;
        this.madre = madre; // puede ser null si no se conoce
    }

    public String getNombre() {
        return nombre;
    }

    public Persona getMadre() {
        return madre;
    }

    @Override
    public String toString() {
        return nombre;
    }
}
```

***

# ✅ `main()` con un ejemplo familiar (nieto → madre → abuela)

```java
public class Main {
    public static void main(String[] args) {
        Persona abuela = new Persona("Carmen", null);
        Persona madre  = new Persona("Laura", abuela);
        Persona nieto  = new Persona("Miguel", madre);

        System.out.println("Nieto: " + nieto);
        System.out.println("Madre del nieto: " + nieto.getMadre());
        System.out.println("Abuela del nieto: " + nieto.getMadre().getMadre());
    }
}
```

Salida aproximada:

    Nieto: Miguel
    Madre del nieto: Laura
    Abuela del nieto: Carmen

***

# ✅ Explicación

En una composición recursiva, un objeto contiene otro objeto del mismo tipo, creando una estructura encadenada. En el ejemplo presentado, cada `Persona` contiene opcionalmente una referencia a su madre, que es otra `Persona`, permitiendo formar árboles genealógicos. Este patrón se replica en estructuras como nodos de árboles, listas enlazadas o directorios del sistema de archivos, donde cada objeto contiene referencias de su mismo tipo para crear formas más complejas.

El uso de inmutabilidad asegura que una vez creada una persona, ni su nombre ni su identidad familiar pueden modificarse. Esto evita inconsistencias lógicas en la estructura, lo que es especialmente útil en modelos con relaciones jerárquicas o históricas. La estructura resultante es estable y libre de efectos secundarios, favoreciendo un diseño más seguro y predecible.

El ejemplo del `main` muestra cómo esta composición recursiva permite representar generaciones de forma natural. El nieto referencia a su madre, y su madre referencia a su abuela, formando una cadena hacia atrás. La recursividad se observa al navegar por los métodos `getMadre()`, que permiten acceder sucesivamente a las ascendientes de una persona, siempre que existan. Esta forma de recorrer estructuras recursivas es habitual en la orientación a objetos.

***

# ✅ Otros ejemplos clásicos de **composiciones recursivas**

Aquí se listan algunos de los ejemplos más comunes:

*   **Listas enlazadas**, donde cada nodo contiene un valor y una referencia al siguiente nodo.
*   **Árboles binarios**, donde cada nodo tiene referencias a sus nodos hijos.
*   **Directorios y archivos**, donde un directorio contiene otros directorios o archivos del mismo tipo base.
*   **Escenas gráficas (scene graphs)**, donde un nodo puede contener una lista de nodos hijos.
*   **Expresiones aritméticas**, donde una expresión puede contener subexpresiones (por ejemplo, nodos de un AST).

## 11. ¿Qué son las relaciones de composición "bidireccionales"? ¿Qué habría que hacer para implementar este tipo de relación en el ejemplo de `Profesor` y `Departamento`?

### Respuesta

Las **relaciones de composición bidireccionales** son aquellas en las que *cada clase mantiene una referencia hacia la otra*, formando así un vínculo en ambos sentidos. A diferencia de una composición unidireccional —donde solo el contenedor conoce a los contenidos—, en una relación bidireccional ambos extremos se “ven”. Esto puede resultar útil cuando ambas clases necesitan conocerse mutuamente para trabajar de forma coherente, pero introduce complejidad, especialmente para mantener la integridad de la relación sin inconsistencias. En este tipo de diseño es esencial evitar estados parciales: si uno apunta al otro, el otro debe apuntar también al primero de forma sincronizada.

En el ejemplo de `Profesor` y `Departamento`, implementar una relación bidireccional implicaría que **cada profesor tendría también un atributo que referencia a su departamento**. De esta manera, el departamento sabría qué profesores pertenecen a él, y cada profesor sabría en qué departamento trabaja. Esto requiere añadir un atributo del tipo `Departamento` en la clase `Profesor`, junto con un método para establecer el departamento de manera controlada. La clave radica en que cualquier modificación en un lado debe actualizarse en el otro lado automáticamente para mantener la coherencia estructural.

Si se implementara esta bidireccionalidad, cada vez que el departamento añadiera un profesor, debería llamarse internamente a un método del profesor para asignarle el departamento. De igual modo, al eliminar un profesor del departamento, habría que poner su referencia a `null` o moverlo a otro departamento si así se estableciera. Este mantenimiento recíproco debe hacerse dentro de las clases implicadas y nunca dejar en manos del usuario la sincronización, porque se correría el riesgo de romper la relación y dejar referencias inconsistentes.

Este tipo de diseño obliga también a pensar en los invariantes adicionales. Por ejemplo, el director debería tener como departamento el mismo en el que está inscrito; y cualquier cambio de director debería seguir respetando la sincronización en ambas direcciones. En general, las relaciones bidireccionales exigen más disciplina, porque requieren garantizar que cada actualización afecta a ambos extremos. Dependiendo del modelo, puede resultar conveniente, pero también puede incrementar el acoplamiento entre clases, por lo que se recomienda emplearlas únicamente cuando sean realmente necesarias.

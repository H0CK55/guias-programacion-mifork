<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Aspectos funcionales". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: clases y objetos, encapsulación, excepciones, composición, herencia, polimorfismo y genericidad.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 7. Aspectos funcionales

## 1. ¿Qué es un puntero a una función? Pon un ejemplo de código en C, donde se define una función y que reciba una cadena de caracteres como parámetro y devuelva la cadena en mayúsculas. Crea un puntero en una variable local a dicha función llamado `aMayusculas` e invócala con el puntero.

### Respuesta

Un puntero a función es una variable que no apunta a datos, sino a código ejecutable, es decir, a una función concreta. Permite almacenar la dirección de una función y llamarla indirectamente, lo que posibilita pasar funciones como parámetros o seleccionar comportamientos en tiempo de ejecución.
En C, los punteros a función son habituales para implementar callbacks o comportamientos configurables, aunque su sintaxis resulta poco intuitiva y no existe ninguna noción de contexto o estado asociado a la función.

#include <stdio.h>
#include <ctype.h>

void aMayusculas(char* s) {
    for (int i = 0; s[i]; i++) {
        s[i] = toupper(s[i]);
    }
}

int main() {
    void (*aMayusculasPtr)(char*) = aMayusculas;
    char texto[] = "hola mundo";
    aMayusculasPtr(texto);
    printf("%s\n", texto);
}


## 2. ¿Qué es una **función lambda** en un lenguaje de programación? Pon un ejemplo similar al anterior en Javascript y otro en Java con funciones lambda. Usa una variable local `aMayusculas` para apuntar a la función lambda. Por simplicidad, en Java, emplea `Function<String, String>` para el tipo de la referencia a la función lambda.

### Respuesta

Una función lambda es una función anónima, definida de forma concisa y que puede asignarse a una variable o pasarse como argumento. A diferencia de una función tradicional, no necesita nombre y suele definirse en el lugar donde se usa.
En JavaScript, las funciones son ciudadanos de primera clase desde el inicio del lenguaje. En Java, las lambdas aparecen a partir de Java 8 y se expresan mediante interfaces funcionales.

let aMayusculas = s => s.toUpperCase();
console.log(aMayusculas("hola"));
``

Function<String, String> aMayusculas = s -> s.toUpperCase();
System.out.println(aMayusculas.apply("hola"));

## 3. ¿Qué es el **paradigma funcional**? ¿Por qué a algunos lenguajes orientados a objetos como Java 8, se les llama multi-paradigma? ¿Qué quiere decir que las funciones son "ciudadanos de primera clase"?

### Respuesta

El paradigma funcional se basa en el uso de funciones puras, la ausencia de efectos secundarios y la composición de funciones para construir comportamiento. Se centra más en qué se quiere hacer que en cómo hacerlo paso a paso.
Lenguajes como Java se consideran multi‑paradigma porque, aunque nacieron como orientados a objetos, incorporan elementos funcionales como lambdas, funciones de orden superior o programación declarativa con streams. Decir que las funciones son ciudadanos de primera clase significa que pueden almacenarse en variables, pasarse como parámetros y devolverse como resultado.

## 4. Explica la sintaxis básica de una función lambda en Java.

### Respuesta

La sintaxis básica de una lambda en Java consta de tres partes: los parámetros, el operador -> y el cuerpo de la función. Si el cuerpo tiene una sola expresión, no es necesario usar llaves ni la palabra return.
Los tipos de los parámetros pueden omitirse si el compilador puede inferirlos a partir del contexto, lo que contribuye a una sintaxis más concisa pero manteniendo el chequeo estático de tipos.

(parametro) -> expresion
(parametro) -> { instrucciones; }
``

## 5. Ahora recibamos una función como parámetro a un método y la llamaremos desde dentro. Amplia los ejemplos anteriores de Java y JavaScript con un método llamado `transformar`, que reciba un `String` como parámetro y luego una función transformadora como lo es `aMayúsculas` y la invoque desde dentro.

### Respuesta

Una de las ideas clave del enfoque funcional es pasar funciones como argumentos a otras funciones. Esto permite parametrizar el comportamiento de un método sin necesidad de herencia ni clases auxiliares.

function transformar(texto, funcion) {
    return funcion(texto);
}

transformar("hola", aMayusculas);

static String transformar(String texto, Function<String, String> f) {
    return f.apply(texto);
}

transformar("hola", aMayusculas);


## 6. Ahora, invoca `transformar`, con una nueva función lambda directamente en la llamada a `transformar`, por ejemplo, una función lambda que invierta la cadena. Define la función de inversión justo cuando la estás pasando como parámetro.

### Respuesta

Las lambdas pueden definirse directamente en el lugar donde se necesitan, sin asignarlas previamente a una variable. Esto favorece un estilo más declarativo y expresivo.

transformar("hola", s -> new StringBuilder(s).reverse().toString());


## 7. ¿Qué se entiende por cierre o "closure" en el contexto de las funciones lambda? Pon un ejemplo en Java de cómo una función lambda es capaz de acceder a una variable local en el contexto donde fue definida. Modifica el ejemplo anterior, creando otra función lambda para transformar una cadena, pero que lo que haga es concatenar a la cadena de entrada otra cadena que está en una variable local definida fuera de la función lambda.

### Respuesta

Un closure se produce cuando una función lambda captura y utiliza variables definidas en su contexto exterior. En Java, estas variables deben ser efectivamente finales, es decir, no modificarse tras su inicialización.   

String sufijo = "!!!";
Function<String, String> f = s -> s + sufijo;
System.out.println(f.apply("hola"));

La lambda recuerda el valor de sufijo incluso cuando se ejecuta fuera del bloque donde fue definida.


## 8. Reflexiona: ¿en qué se diferencia entonces una función lambda de los punteros a funciones que hay en C?

### Respuesta

La diferencia fundamental es que una lambda es un objeto con comportamiento, mientras que un puntero a función es solo una dirección de código. Las lambdas pueden capturar estado (closures), cumplir interfaces y participar en el sistema de tipos.
En C, no existe el concepto de cierre ni integración con tipos, por lo que los punteros a función son más limitados y propensos a errores.

## 9. Devolvamos ahora funciones. Creemos ahora una función que sea capaz de crear funciones "descuento". Una función "descuento", decrementa un porcentaje pasado como parámetro. Por simplicidad, usa `Function<Double, Double>` para su tipo. La función `crearDescuento(porcentaje)`, recibe solo el porcentaje de descuento a aplicar y devuelve la función de descuento. Prueba a crear dos descuentos distintos y aplicarlos a una cantidad. Explica la closure en la función descuento.

### Respuesta

Las funciones pueden devolverse como resultado, creando comportamientos personalizados. En este ejemplo, la función devuelta recuerda el porcentaje de descuento gracias a un closure.

static Function<Double, Double> crearDescuento(double porcentaje) {
    return precio -> precio * (1 - porcentaje);
}

Function<Double, Double> d10 = crearDescuento(0.10);
Function<Double, Double> d20 = crearDescuento(0.20);

System.out.println(d10.apply(100.0));
System.out.println(d20.apply(100.0));
``

## 10. En Java, que es un lenguaje con comprobación estática de tipos, donde los tipos se declaran, toda función lambda tiene un tipo, que se conoce como **interfaz funcional**. ¿Qué es una **interfaz funcional**? ¿Qué requisitos tiene?

### Respuesta

Una interfaz funcional es una interfaz que declara exactamente un método abstracto. Esto permite que una expresión lambda tenga un tipo bien definido en un lenguaje con tipado estático como Java.
Puede contener métodos default o static, pero solo un método abstracto. Ejemplos comunes son Runnable, Function o Comparator.

## 11. Creemos una interfaz funcional a mano. Por ejemplo, define la interfaz funcional del ejemplo que transforma la cadena en otra. Llámale `Transformador`, que define una función que convierte una cadena de texto (`String`) en otra (`String`).

### Respuesta

@FunctionalInterface
public interface Transformador {
    String transformar(String s);
}

Esta interfaz puede usarse para definir cualquier transformación de cadenas mediante lambdas.

## 12. Ahora hagamos la interfaz funcional algo más genérica y empleando generics, para que permita definir un `Transformador` de un tipo en otro. Pon un ejemplo de un transformador que redondea un `Double` en un `Integer`.

### Respuesta

Mediante generics, la interfaz se hace reutilizable para cualquier tipo de transformación.

@FunctionalInterface
public interface Transformador<T, R> {
    R transformar(T valor);
}

Transformador<Double, Integer> redondear = d -> d.intValue();


## 13. `Transformador`, en su versión genérica, parece muy útil y reutilizable, hasta el punto de que es igual a una interfaz funcional que ya hay, que es `Function<T, R>`. Muestra las interfaces funcionales predefinidas que hay en Java.

### Respuesta

Java proporciona numerosas interfaces funcionales en java.util.function, como Function<T,R>, Consumer<T>, Supplier<T>, Predicate<T>, UnaryOperator<T> y BinaryOperator<T>. Cubren los casos funcionales más habituales sin necesidad de crear interfaces nuevas.


## 14. Vamos a ver ejemplos expresivos de funcional en Java. Estudiemos el `List.forEach`, como versión funcional del bucle `for`. Emplea el `forEach` para recorrer una lista de `Integer` y que muestre un mensaje si el entero es positivo.

### Respuesta

List<Integer> lista = List.of(1, -2, 3, -4);

lista.forEach(n -> {
    if (n > 0) {
        System.out.println("Positivo: " + n);
    }
});

Este enfoque expresa directamente la intención sin gestionar índices ni bucles explícitos.

## 15. Repasando el tema de genericidad, fíjate en la firma de `forEach`, ¿por qué se usa `Consumer<? super T>` y no `Consumer<T>`? Explica qué significa **PECS**, y explícalo para el caso de mejorar el ejemplo del método `transformar` la hora de definir el tipo de la función transformadora.

### Respuesta

La firma de forEach usa Consumer<? super T> porque el consumidor consume elementos. Según el principio PECS (Producer Extends, Consumer Super), cuando se consumen valores debe usarse super, y cuando se producen, extends.
Aplicado al método transformar, si la función produce un valor a partir de T, se usaría Function<? super T, ? extends R> para maximizar flexibilidad y seguridad de tipos.

## 16. Referencias a métodos. Podemos obtener una referencia a métodos de objetos o clases. Pon un ejemplo en JavaScript y en Java, de una clase `Persona` con un método `saludar`. En el código principal, crea una `Persona` con un nombre, y obtén una referencia a su método `saludar` en una variable local. Invoca `saludar` con esa referencia a su método `saludar`.

### Respuesta

class Persona {
  constructor(nombre) { this.nombre = nombre; }
  saludar() { console.log("Hola soy " + this.nombre); }
}

let p = new Persona("Ana");
let f = p.saludar.bind(p);
f();
``
class Persona {
    String nombre;
    Persona(String n) { nombre = n; }
    void saludar() { System.out.println("Hola soy " + nombre); }
}

Persona p = new Persona("Ana");
Runnable r = p::saludar;
r.run();    


## 17. ¿Qué tipos de referencias a método se pueden hacer en Java? Pon un ejemplo de referencia a método estático, a constructor, a método de instancia de una instancia concreta y a método de instancia sobre cualquier instancia.

### Respuesta


// Método estático
Function<String, Integer> f1 = Integer::parseInt;

// Constructor
Supplier<List<String>> f2 = ArrayList::new;

// Método de instancia concreto
Persona p = new Persona("Luis");
Runnable f3 = p::saludar;

// Método de instancia sobre cualquier objeto
Function<String, Integer> f4 = String::length;
``

## 18. Otro ejemplo expresivo. Ordena una lista de `Persona`, cada persona tiene un nombre y una edad (de tipo entero). Ordena la lista de `Persona` con `Collections.sort`, pasándole como comparador una expresión lambda que compare la edad de ambas personas y si tienen la misma edad, se ordene por orden alfabético del nombre. Crea dos versiones: Una con la función de comparación hecha manualmente, y otra empleando `Comparator`.

### Respuesta

Collections.sort(personas, (p1, p2) -> {
    int c = Integer.compare(p1.getEdad(), p2.getEdad());
    return c != 0 ? c : p1.getNombre().compareTo(p2.getNombre());
});
------------------------------------------
Collections.sort(
    personas,
    Comparator.comparingInt(Persona::getEdad)
              .thenComparing(Persona::getNombre)
);

La segunda versión es más declarativa, legible y reutiliza utilidades estándar del lenguaje.
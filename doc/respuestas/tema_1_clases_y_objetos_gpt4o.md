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

### Respuesta
🔹1. Encapsulamiento
Consiste en ocultar los detalles internos de un objeto y permitir el acceso solo mediante métodos públicos (getters, setters, etc.).
Protege los datos y evita que se modifiquen directamente desde fuera del objeto.
Idea clave: mantener los datos seguros y controlar cómo se usan.

🔹 2. Abstracción
Permite simplificar la realidad, mostrando únicamente lo esencial y ocultando lo innecesario.
Un objeto ofrece solo las operaciones relevantes sin mostrar la lógica interna.
Idea clave: enfocarse en qué hace un objeto, no en cómo lo hace.

🔹 3. Herencia
Es el mecanismo por el cual una clase puede heredar atributos y métodos de otra clase.
Permite reutilizar código y establecer relaciones jerárquicas (clase padre → clase hija).
Idea clave: reutilización y especialización.

🔹 4. Polimorfismo
Permite que un mismo método tenga comportamientos diferentes según el objeto que lo utilice.
Las clases hijas pueden redefinir métodos de la clase padre (sobrescritura).
Idea clave: un mismo mensaje → diferentes respuestas.

## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Respuesta
🔹C++ – Uno de los lenguajes clásicos de POO; combina programación estructurada y orientada a objetos.
🔹Java – Totalmente orientado a objetos, muy usado en aplicaciones empresariales y Android.
🔹Python – Lenguaje multiparadigma que soporta POO de forma sencilla y flexible.
🔹C# – Orientado a objetos, muy utilizado en desarrollo de videojuegos (Unity) y aplicaciones .NET.

## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### Respuesta
🔷 ¿Qué es la programación estructurada?
La programación estructurada es un paradigma que organiza el código usando estructuras de control bien definidas, evitando el uso excesivo de saltos como goto.
Su objetivo principal es que el programa sea más fácil de leer, entender y mantener.
Se basa en tres estructuras fundamentales:

Secuencia → instrucciones que se ejecutan en orden.
Selección → decisiones (if, switch).
Iteración → bucles (for, while).

📌 Idea clave:

“Dividir un programa en bloques lógicos claros, sin caos ni saltos descontrolados.”

Lenguajes típicos: C, Pascal, Ada…

🔷 ¿Qué es la programación modular?
La programación modular es un enfoque donde el programa se divide en módulos independientes, cada uno encargado de una tarea concreta.
Estos módulos pueden ser funciones, archivos separados, bibliotecas, etc.
Sus objetivos principales:

Reutilización de código.
Facilidad de mantenimiento (cambias un módulo sin romper el resto).
Trabajo en equipo más ordenado (cada persona programa un módulo).
Reducción de complejidad, al dividir un problema grande en partes pequeñas.

📌 Idea clave:

“Dividir el programa en piezas reutilizables y organizadas, cada una especializada en una tarea.”

Lenguajes típicos: C, Modula-2, Python (gracias a módulos y paquetes), etc.

🧩 ¿Cómo se relacionan?

La programación estructurada organiza el flujo del programa.
La programación modular organiza la arquitectura del programa.

Juntas establecieron las bases de la POO, que añadió la idea de objetos que combinan datos y funciones.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Respuesta
🔹 1. Atributos (o propiedades)
Son los datos que describen el estado del objeto.
Representan sus características.
Ejemplo:
Un objeto Coche podría tener atributos como color, velocidad, marca.

🔹 2. Métodos (o comportamientos)
Son las acciones que el objeto puede realizar.
Definen cómo se comporta y cómo interactúa con otros objetos.
Ejemplo:
El Coche podría tener métodos como acelerar(), frenar(), girar().

🔹 3. Identidad
Es lo que hace que cada objeto sea único, incluso aunque tenga los mismos atributos y métodos que otro.
En la práctica, es la referencia en memoria que distingue a un objeto de otro.
Ejemplo:
Dos coches idénticos (mismo color, marca, etc.) siguen siendo objetos diferentes.

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Respuesta
🔷 ¿Qué es una clase?
Una clase es un modelo o plantilla a partir del cual se crean objetos.
Define qué atributos (datos) y qué métodos (comportamientos) tendrán esos objetos.
📌 Idea clave:

La clase es como un plano; los objetos son las casas construidas con ese plano.

🔷 ¿Es lo mismo una clase que un objeto?
No.
Una clase es solo el diseño, mientras que un objeto es un ejemplar real creado a partir de esa clase.

Clase → concepto, definición.
Objeto → cosa concreta en memoria.


🔷 ¿Qué es una instancia?
Una instancia es simplemente un objeto creado a partir de una clase.
El proceso se llama instanciación.

🔷 ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?
No.
Aunque muchos lenguajes orientados a objetos están basados en clases (C++, Java, C#, Python, etc.), no todos usan clases como elemento fundamental.
Existen dos modelos principales:

🔹 1. Lenguajes basados en clases
La mayoría de los OOP populares:

C++
Java
C#
Python (tiene clases, aunque también soporta objetos sin clase en versiones antiguas)
Ruby


🔹 2. Lenguajes basados en prototipos (sin clases tradicionales)
Estos lenguajes no usan clases, sino que crean objetos a partir de otros objetos llamados prototipos.
Ejemplos:

JavaScript
Lua
Self
Io

En JavaScript, por ejemplo, las clases eran inexistentes originalmente; lo que existen realmente son prototipos, aunque desde ES6 haya una sintaxis de “class” por comodidad.
📌 Idea clave:

Un lenguaje puede ser orientado a objetos sin necesidad de tener clases.

## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### Respuesta
📍 ¿Dónde se almacenan los objetos en Java?
En Java, los objetos (instancias) se crean en el heap.
Lo que guardas en las variables son referencias (apuntadores) a esos objetos.
Las variables locales (incluidas las referencias) viven en la pila (stack) dentro del frame del método.

🔁 ¿Es igual en todos los lenguajes?
No. Pero como estás en Java, quédate con esto:

En Java, casi todo objeto vive en el heap y se accede mediante referencias.
Algunas optimizaciones del JIT (como escape analysis) pueden eliminar asignaciones al heap y scalarizar objetos temporalmente, pero conceptualmente para ti el objeto es de heap.
Los tipos primitivos (int, double, boolean, etc.) no son objetos y pueden almacenarse directamente en el stack (si son locales) o embebidos en campos.
Sus wrappers (Integer, Double, …) sí son objetos en el heap.


🧹 ¿Qué es la recolección de basura (Garbage Collection, GC) en Java?
El GC es un mecanismo automático que:

Detecta qué objetos ya no son alcanzables (no hay referencias vivas que puedan llegar a ellos).
Libera su memoria en el heap sin que tú tengas que llamar a free() o delete.

¿Cómo funciona a grandes rasgos?

Java usa coleccionado generacional: objetos nuevos van a la Generación Joven (Eden/Survivor).
Si sobreviven varias colecciones, “promocionan” a la Generación Antigua.
El GC hace fases de marcado (mark) para ver qué está vivo y barrido/compactación (sweep/compact) para recuperar memoria y reducir fragmentación.
Existen varios coleccionadores (según versión/flags): Serial, Parallel, CMS (deprecated), G1 (por defecto en Java modernos), ZGC, Shenandoah (pausas muy bajas).


Tú no controlas cuándo corre el GC, pero puedes sugerir con System.gc() (no garantizado).
Lo normal es no llamarlo; deja que la JVM decida.

## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### Respuesta
🔷 ¿Qué es un método?
Un método es una función dentro de una clase.
Define un comportamiento que los objetos de esa clase pueden realizar.
Permite encapsular acciones, cálculos o lógica relacionada con los datos del objeto.
📌 Es el “qué sabe hacer” un objeto.

🔷 ¿Qué es la sobrecarga de métodos (method overloading)?
La sobrecarga de métodos consiste en definir varios métodos con el mismo nombre pero con diferentes parámetros.
Los métodos sobrecargados se diferencian por:

número de parámetros
tipo de parámetros
orden de los parámetros

📌 No cambia el nombre del método, solo su “forma de llamarlo”.
📌 No es lo mismo que sobrescritura (override). La sobrecarga ocurre en la misma clase.

## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### Respuesta
✅ Clase Punto mínima
-----------------------------------
class Punto {
    int x;   // visibilidad por defecto (package-private)
    int y;   // igual que arriba

    double calculaDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}
-----------------------------------
✅ Ejemplo de uso
-----------------------------------
public class Demo {
    public static void main(String[] args) {
        Punto p = new Punto();
        p.x = 3;
        p.y = 4;

        double d = p.calculaDistanciaAOrigen();
        System.out.println("Distancia al origen: " + d);
    }
}
-----------------------------------
✔ Qué imprime
El punto (3,4) tiene una distancia al origen de 5.0, siguiendo el teorema de Pitágoras.

## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### Respuesta
🔷 ¿Cuál es el punto de entrada en un programa en Java?
El punto de entrada es el método main con la firma exacta:
------------------------------------
public static void main(String[] args)
------------------------------------
Cuando ejecutas un programa Java, la JVM busca esa firma exacta en la clase que se lanza.

🔷 ¿Qué es static y para qué sirve?
static significa:
👉 El miembro pertenece a la clase, no a las instancias.

Un método static se puede llamar sin crear un objeto.
Un atributo static es compartido por todas las instancias.

Ejemplo:
------------------------------------
class Contador {
    static int total = 0;  // compartido por todos los objetos
}
------------------------------------
🔷 ¿Solo se emplea para el método main?
No.
static se usa en muchos sitios:
✔ Atributos estáticos
Valores compartidos entre todos los objetos.
------------------------------------
static int contador;
------------------------------------
✔ Métodos estáticos
Acciones que no dependen del estado de una instancia.
------------------------------------
static void imprimirHola() {
    System.out.println("Hola");
}
------------------------------------
✔ Bloques estáticos
Se ejecutan UNA vez al cargar la clase.
------------------------------------
static {
    System
------------------------------------
✔ Clases internas estáticas
Usadas en patrones como Builder o Singleton.

🔷 ¿Para qué se combina con final?
La combinación static final suele usarse para constantes.

🧩 ¿Qué hace final?
final significa:

En variables → no se puede cambiar el valor.
En métodos → no se pueden sobrescribir (override).
En clases → no se pueden heredar.
------------------------------------
final int x = 10;     // no se puede cambiar
final class A {}      // no se puede extender
------------------------------------
🔷 ¿Qué significa static final?
Significa que:

static → la constante pertenece a la clase
final → su valor no cambia
Se escribe normalmente en mayúsculas por convención
------------------------------------
class Matematicas {
    static final double PI = 3.141592653589793;
}
------------------------------------
Acceso:
------------------------------------
double r = Matematicas.PI;
------------------------------------

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Respuesta

# 🔷 1. ¿Cómo compilar un programa Java desde la línea de comandos?

Supón que tienes un archivo llamado:

    Hola.java

con el siguiente contenido:

```java
public class Hola {
    public static void main(String[] args) {
        System.out.println("Hola, Java!");
    }
}
```

### ✔ Paso 1: Compilar con `javac`

```bash
javac Hola.java
```

Esto crea un archivo:

    Hola.class

***

# 🔷 2. ¿Cómo ejecutar el programa?

Usas el comando `java` **sin poner la extensión `.class`**:

```bash
java Hola
```

Salida:

    Hola, Java!

***

# 🔷 3. ¿Java es compilado?

La respuesta correcta es:

## ✔ Java es **compilado** *y* **interpretado**.

### ✔ Etapa 1 → Compilación

El compilador `javac` convierte el código `.java` en **bytecode**, que se guarda en archivos `.class`.

### ✔ Etapa 2 → Interpretación / ejecución en la JVM

La **máquina virtual Java** (JVM) toma ese bytecode y:

*   lo interpreta
*   y/o lo recompila en caliente a código nativo (con JIT)

Por eso se dice que Java es un **lenguaje híbrido**:

> *Compila a bytecode, luego la JVM lo ejecuta.*

***

# 🔷 4. ¿Qué es la **máquina virtual Java** (JVM)?

La JVM es un **programa** que se encarga de ejecutar el bytecode Java.  
Es una especie de “mini-ordenador virtual” que simula una CPU idealizada.

Funciones de la JVM:

*   Ejecutar bytecode
*   Manejar memoria
*   Hacer *garbage collection*
*   Proveer seguridad
*   Abstraer del sistema operativo (por eso Java es portable)

📌 *Esa frase típica de Java viene de aquí:*

> “Write once, run anywhere”

***

# 🔷 5. ¿Qué es el **bytecode**?

El bytecode es el **lenguaje intermedio** generado por `javac`.  
No es código máquina real, pero tampoco código fuente.

Características:

*   Es independiente del sistema operativo.
*   Se ejecuta en la JVM, no directamente en tu CPU.
*   Es más eficiente que interpretar código fuente.

Ejemplo ilustrativo (simplificado):

Si el archivo es:

```java
System.out.println("Hola");
```

El bytecode traducido puede contener instrucciones como:

    getstatic java/lang/System/out
    ldc "Hola"
    invokevirtual java/io/PrintStream/println

La JVM sabe interpretar esas instrucciones.

***

# 🔷 6. ¿Qué son los ficheros `.class`?

Son los archivos que contienen **bytecode compilado**.  
Por ejemplo, si tienes:

    Hola.java

y compilas con:

    javac Hola.java

obtendrás:

    Hola.class

Ese `.class` contiene el bytecode que ejecutará la JVM.


## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Respuesta

# 🔷 ¿Qué es `new` en Java?

`new` es un **operador** que sirve para **crear objetos** en Java.

Cuando haces:

```java
Punto p = new Punto();
```

sucede lo siguiente:

1.  Se reserva memoria en el **heap** para el nuevo objeto.
2.  Se llama al **constructor** de la clase.
3.  La expresión `new Punto()` devuelve una **referencia** al objeto recién creado.
4.  Esa referencia se guarda en la variable `p`.

📌 *Idea clave:*

> `new` crea un objeto en memoria y ejecuta su constructor.

***

# 🔷 ¿Qué es un **constructor** en Java?

Un **constructor** es un **método especial** que sirve para **inicializar** los objetos de una clase.

Características de un constructor:

*   Tiene **el mismo nombre que la clase**.
*   **No tiene tipo de retorno**, ni siquiera `void`.
*   Se ejecuta automáticamente cuando haces `new Clase(...)`.
*   Sirve para inicializar atributos o ejecutar código de preparación.

Ejemplo general:

```java
class Ejemplo {
    Ejemplo() {
        // código de inicialización
    }
}
```

También existen **constructores con parámetros**, que permiten crear objetos con valores iniciales personalizados.

***

# 🔷 Ejemplo: Constructor en una clase `Empleado`

Creamos una clase `Empleado` con tres atributos:

*   `dni`
*   `nombre`
*   `apellidos`

✔ Incluimos un **constructor** que reciba esos tres valores.

```java
class Empleado {
    String dni;
    String nombre;
    String apellidos;

    // Constructor
    Empleado(String dni, String nombre, String apellidos) {
        this.dni = dni;
        this.nombre = nombre;
        this.apellidos = apellidos;
    }
}
```

### ¿Qué es `this`?

`this` es una referencia al **objeto actual**, y se usa aquí para distinguir entre:

*   el atributo `dni`
*   el parámetro `dni`

***

# 🔷 Ejemplo de uso del constructor

```java
public class Demo {
    public static void main(String[] args) {

        Empleado e = new Empleado("12345678A", "Alonso", "Fernández Rodríguez");

        System.out.println("Empleado:");
        System.out.println(e.nombre + " " + e.apellidos + " — DNI: " + e.dni);
    }
}
```

Salida esperada:

    Empleado:
    Alonso Fernández Rodríguez — DNI: 12345678A


## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### Respuesta

# 🔷 ¿Qué es la referencia `this`?

En Java, `this` es una **referencia al objeto actual**, es decir, al **objeto sobre el que se está ejecutando el método**.

Sirve para:

*   Distinguir entre **atributos** y **parámetros** del mismo nombre.
*   Pasar una referencia del objeto actual a otros métodos o constructores.
*   Encadenar constructores usando `this(...)`.
*   Acceder al propio objeto dentro de un método.

📌 *Idea clave:*

> `this` apunta al objeto actual en el heap.

***

# 🔷 ¿Se llama igual en todos los lenguajes?

No exactamente.

Muchos lenguajes orientados a objetos usan un nombre equivalente, pero no todos usan `this`.

*   **Java →** `this`
*   **JavaScript →** `this` (pero mucho más complejo)
*   **C++ →** `this` (puntero, no referencia)
*   **C# →** `this`
*   **Python →** usa `self` (pero no es palabra reservada; solo una convención)
*   **Rust →** no usa `this`, maneja el objeto de otra forma
*   **Swift →** `self`

📌 Lo común es que cada objeto tenga una forma de referirse a sí mismo, pero **no siempre se llama igual y no siempre funciona igual**.

***

# 🔷 Ejemplo del uso de `this` en la clase `Punto`

Vamos a modificar tu clase `Punto` para añadir un **constructor** y utilizar `this` para distinguir entre atributos y parámetros del mismo nombre.

```java
class Punto {
    int x;   // atributo
    int y;   // atributo

    // Constructor usando this
    Punto(int x, int y) {
        this.x = x;   // 'this.x' es el atributo; 'x' es el parámetro
        this.y = y;
    }

    double calculaDistanciaAOrigen() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
        // 'this' es opcional aquí, pero deja claro que accedemos al objeto
    }
}
```

***

### ✔ Ejemplo de uso

```java
public class Demo {
    public static void main(String[] args) {
        Punto p = new Punto(3, 4);
        System.out.println(p.calculaDistanciaAOrigen()); // 5.0
    }
}
```

## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Respuesta

# ✅ Clase `Punto` con el nuevo método `distanciaA`

```java
class Punto {
    int x;
    int y;

    Punto(int x, int y) {
        this.x = x;
        this.y = y;
    }

    double calculaDistanciaAOrigen() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
    }

    // Nuevo método
    double distanciaA(Punto otro) {
        int dx = this.x - otro.x;
        int dy = this.y - otro.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}
```

***

# 🔍 Explicación rápida

*   `this.x` y `this.y` → coordenadas del objeto actual.
*   `otro.x` y `otro.y` → coordenadas del punto recibido.
*   Usamos la fórmula de distancia entre dos puntos:


# ▶ Ejemplo de uso

```java
public class Demo {
    public static void main(String[] args) {
        Punto p1 = new Punto(3, 4);
        Punto p2 = new Punto(0, 0);

        System.out.println("Distancia de p1 a origen: " + p1.calculaDistanciaAOrigen());
        System.out.println("Distancia entre p1 y p2: " + p1.distanciaA(p2));
    }
}
```

Salida:

    Distancia de p1 a origen: 5.0
    Distancia entre p1 y p2: 5.0


## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### Respuesta

# 🔷 1. ¿El paso de un `Punto` como parámetro es **por copia** o **por referencia**?

En **Java**, *todo* se pasa por **valor**.  
Pero hay que entender **qué valor se copia**.

### ✔ Cuando pasas un objeto (como `Punto`), Java copia **el valor de la referencia**.

Eso significa:

*   Dentro del método, el parámetro apunta al **mismo objeto** que fuera.
*   Si modifies **atributos** del objeto, los cambios afectan fuera.

📌 *Pero NO se copia el objeto en sí. Solo la referencia.*

***

# 🔍 Ejemplo claro

```java
static void mueve(Punto p) {
    p.x = 99;     // esto SÍ afecta al objeto original
    p.y = 88;
}
```

Como `p` apunta al mismo objeto que la variable original, **los cambios se ven fuera**.

***

# 🔷 2. ¿Entonces es paso por referencia?

**NO.**  
Java **no tiene** paso por referencia.

Es:

### 👉 Paso **por valor** de la **referencia**.

La referencia es una especie de “puntero protegido”, y ese *valor* se copia.  
Los dos parámetros apuntan al mismo objeto.

Pero si dentro del método haces esto:

```java
static void reemplaza(Punto p) {
    p = new Punto(0,0);   // NO cambia la variable original
}
```

La referencia original **NO** se modifica.  
Por eso no es “paso por referencia”.

***

# 🔷 3. ¿Qué pasa si en vez de un `Punto` pasamos un `int`?

Los tipos primitivos (`int`, `double`, `boolean`, etc.) **sí se pasan por valor real**.

*   Se copia el **valor**.
*   Los cambios dentro del método **NO afectan fuera**.

Ejemplo:

```java
static void incrementa(int n) {
    n = n + 1;   // solo cambia la copia local
}

public static void main(String[] args) {
    int x = 10;
    incrementa(x);
    System.out.println(x);   // sigue siendo 10
}
```

## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### Respuesta

# 🔷 ¿Qué es el método `toString()` en Java?

`toString()` es un método definido en la clase base `Object`, por lo que **todas las clases en Java lo heredan**.

Sirve para:

*   Devolver una **representación en forma de texto** del objeto.
*   Facilitar depuración, impresión y logging.
*   Hacer que `System.out.println(obj)` muestre algo útil en vez de la referencia en memoria.

Si no lo sobreescribes, su versión por defecto muestra algo así como:

    Punto@3f99bd52

Es decir: nombre de la clase + hash en hexadecimal → totalmente inútil para un humano.

📌 Por eso, **se suele sobrescribir (`override`)**.

***

# 🔷 ¿Existe `toString()` en otros lenguajes?

Sí, casi todos los lenguajes orientados a objetos tienen un sistema similar, aunque **no siempre se llama igual**:

| Lenguaje       | Método equivalente                                 |
| -------------- | -------------------------------------------------- |
| **Java**       | `toString()`                                       |
| **C#**         | `ToString()`                                       |
| **C++**        | No hay método estándar; se sobrecarga `operator<<` |
| **Python**     | `__str__()` y `__repr__()`                         |
| **JavaScript** | `toString()` existe en `Object.prototype`          |
| **Kotlin**     | `toString()`                                       |
| **Ruby**       | `to_s`                                             |

La idea general es la misma: **representar un objeto como texto**.

***

# 🔷 Ejemplo de `toString()` en la clase `Punto`

Aquí tienes una versión limpia y típica:

```java
class Punto {
    int x;
    int y;

    Punto(int x, int y) {
        this.x = x;
        this.y = y;
    }

    double calculaDistanciaAOrigen() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
    }

    double distanciaA(Punto otro) {
        int dx = this.x - otro.x;
        int dy = this.y - otro.y;
        return Math.sqrt(dx * dx + dy * dy);
    }

    @Override
    public String toString() {
        return "(" + this.x + ", " + this.y + ")";
    }
}
```

***

# 🔷 Ejemplo de uso

```java
public class Demo {
    public static void main(String[] args) {
        Punto p = new Punto(3, 4);
        System.out.println(p);            // llama automáticamente a p.toString()
        System.out.println(p.toString()); // lo mismo
    }
}
```

Salida:

    (3, 4)

***

## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?

### Respuesta

# 🔷 ¿Una **clase** es como un `struct` en C?

**Parecido, pero NO es lo mismo.**  
Un `struct` en C se parece a una clase en que ambos:

*   Agrupan datos bajo un mismo tipo.
*   Permiten crear variables basadas en ese tipo (aunque en C no se llaman “instancias”).

Pero **hasta ahí llegan las similitudes**.

***

# 🔷 ¿Qué le falta a un `struct` de C para ser como una clase?

Los `struct` de C solo contienen **datos**, mientras que una clase contiene:

## ✔ 1. **Métodos**

Una clase tiene **comportamientos** asociados (funciones dentro del tipo).  
Un `struct` de C no puede tener funciones “dentro”, solo fuera.

```java
class Punto {
    int x, y;
    double distancia() { return Math.sqrt(x*x + y*y); }
}
```

En C, eso es imposible de expresar dentro del `struct`.

***

## ✔ 2. **Encapsulación** (control de acceso)

Las clases pueden tener:

*   `public`
*   `private`
*   `protected`
*   default/package-private (en Java)

Un `struct` de C **no tiene** control de visibilidad: todos los miembros son públicos y accesibles sin restricciones.

En Java:

```java
class Empleado {
    private String dni;  // imposible hacer algo así en C
}
```

En C:

```c
struct Empleado {
    char dni[10];   // siempre público
};
```

No lo puedes ocultar.

***

## ✔ 3. **Constructores**

Una clase puede inicializar automáticamente sus atributos mediante un **constructor**.

Los `struct` en C **no tienen constructores**.  
Debes inicializar todo “a mano”.

***

## ✔ 4. **Operaciones asociadas a instancias**

Una clase define operaciones que actúan **sobre ese objeto concreto**.

Por ejemplo:

```java
p1.distanciaA(p2);
```

En C no existe el concepto de “método asociado al objeto”.

***

## ✔ 5. **Identidad de objeto**

Un objeto tiene **identidad**, un `struct` es una simple colección de datos.

En C puedes copiar un `struct` y obtienes **una copia completa**, no dos “instancias” distintas en el sentido OO.

Ejemplo:

```c
struct Punto a = {1,2};
struct Punto b = a;  // copia de todos los campos, no referencia
```

En OO no necesariamente ocurre así (normalmente se copian referencias, no los objetos).

***

## ✔ 6. **Herencia**

Las clases pueden extenderse unas de otras (Java, C++, C#, etc.).

Los `struct` de C NO soportan herencia.

***

## ✔ 7. **Polimorfismo asociado a clases**

Java usa clases y referencias para permitir polimorfismo:

```java
Animal a = new Perro();
```

C no puede hacer algo así con `struct`.

***

# 🔷 Entonces... ¿qué le falta exactamente?

## 🧾 Para que un `struct` de C fuese equivalente a una clase OO necesitaría:

1.  **Poder contener funciones internas (métodos)**
2.  **Encapsulación:** soporte de `private`, `public`, etc.
3.  **Constructores**
4.  **Soporte para funciones miembro que operen sobre “this”**
5.  **Identidad (punteros implícitos a sí mismo)**
6.  **Herencia**
7.  **Polimorfismo basado en herencia y tipos**
8.  **Destructores automáticos / gestión de ciclo de vida**
9.  **Sobrecarga de métodos en la propia estructura**
10. **Capacidad para asociar comportamiento y estado de forma unificada**

En resumen:

> Un `struct` de C tiene **solo estado**, una clase en POO tiene **estado + comportamiento + reglas de visibilidad + ciclo de vida + relaciones jerárquicas**.

***

# 🔷 ¿Y si miramos a C++?

C++ sí permite:

*   `struct` con métodos
*   constructores
*   encapsulación
*   herencia
*   etc.

La única diferencia real entre `class` y `struct` en C++ es la visibilidad por defecto.

Pero **la pregunta original era sobre C**, y ahí sí son muy diferentes.


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### Respuesta

La idea clave es:  
**en C no hay métodos ni `this` implícito**, así que **pasamos explícitamente un puntero al `struct`** a las funciones que operan sobre él. Ese puntero hace el papel de `this`.

***

## 1) Versión mínima en C: `struct` + funciones “libres”

### `punto.h`

```c
#ifndef PUNTO_H
#define PUNTO_H

typedef struct {
    int x;
    int y;
} Punto;

/* “Constructor” estilo C (inicializador) */
void punto_init(Punto* p, int x, int y);

/* “Método” que calcula la distancia al origen */
double punto_distancia_origen(const Punto* p);

#endif
```

### `punto.c`

```c
#include "punto.h"
#include <math.h>

void punto_init(Punto* p, int x, int y) {
    p->x = x;
    p->y = y;
}

double punto_distancia_origen(const Punto* p) {
    /* Usamos const para dejar claro que no modificamos el objeto */
    return sqrt((double)p->x * p->x + (double)p->y * p->y);
}
```

### `main.c`

```c
#include <stdio.h>
#include "punto.h"

int main(void) {
    Punto p;                 /* “instancia” en la pila */
    punto_init(&p, 3, 4);    /* “constructor” manual */

    double d = punto_distancia_origen(&p);  /* p hace de 'this' */
    printf("Distancia al origen: %.1f\n", d);  /* 5.0 */

    return 0;
}
```

**¿Qué ha pasado con `this`?**  
En C **no existe** `this`. Lo que hacemos es **pasar un puntero al objeto** (`Punto* p`) como **primer argumento** de cada función que actúa sobre él. Ese puntero **es** nuestro `this` *explícito*.  
En C++/Java ese parámetro es implícito; en C lo pasamos a mano.

***

## 2) ¿Y la “instanciación” y los constructores?

*   En C **no hay `new` ni constructores**.
*   Usamos funciones como `punto_init(Punto* p, ...)` para **inicializar** una variable ya creada (en la pila o en el heap si la reservaste con `malloc`).
*   Si necesitas reservar dinámicamente:

```c
#include <stdlib.h>
#include <stdio.h>
#include <math.h>

typedef struct {
    int x, y;
} Punto;

Punto* punto_create(int x, int y) {
    Punto* p = (Punto*)malloc(sizeof(Punto));
    if (p) { p->x = x; p->y = y; }
    return p;
}

void punto_destroy(Punto* p) {
    free(p);
}

double punto_distancia_origen(const Punto* p) {
    return sqrt((double)p->x * p->x + (double)p->y * p->y);
}

int main(void) {
    Punto* p = punto_create(3, 4);
    if (!p) return 1;

    printf("%.1f\n", punto_distancia_origen(p));  // 5.0
    punto_destroy(p);
    return 0;
}
```

Aquí **tú gestionas la memoria** (`malloc`/`free`), al contrario que en Java (GC).

***

## 3) Encapsulación “a la C”: `opaque structs` (opcional, nivel pro)

C no tiene `private/public`, pero puedes **ocultar los campos** usando un **puntero a estructura opaca** en el `.h`.

### `punto.h` (interfaz pública)

```c
#ifndef PUNTO_H
#define PUNTO_H

/* Declaración incompleta: oculta los campos al usuario de la API */
typedef struct Punto Punto;

Punto* punto_create(int x, int y);
void   punto_destroy(Punto* p);

int    punto_get_x(const Punto* p);
int    punto_get_y(const Punto* p);
void   punto_set(Punto* p, int x, int y);

double punto_distancia_origen(const Punto* p);

#endif
```

### `punto.c` (implementación privada)

```c
#include "punto.h"
#include <stdlib.h>
#include <math.h>

/* Definición real, solo visible aquí */
struct Punto {
    int x, y;
};

Punto* punto_create(int x, int y) {
    Punto* p = (Punto*)malloc(sizeof(Punto));
    if (p) { p->x = x; p->y = y; }
    return p;
}

void punto_destroy(Punto* p) { free(p); }

int  punto_get_x(const Punto* p) { return p->x; }
int  punto_get_y(const Punto* p) { return p->y; }
void punto_set(Punto* p, int x, int y) { p->x = x; p->y = y; }

double punto_distancia_origen(const Punto* p) {
    return sqrt((double)p->x * p->x + (double)p->y * p->y);
}
```

Con esto **simulas encapsulación**: el usuario **no puede acceder a `x`/`y` directamente**, solo mediante funciones.

***

## 4) Alternativa: “métodos” dentro del `struct` con punteros a función (estilo vtable)

No es necesario, pero educativo:

```c
#include <math.h>

typedef struct Punto Punto;

typedef struct {
    double (*distancia_origen)(const Punto* self);
} PuntoVTable;

struct Punto {
    int x, y;
    const PuntoVTable* vptr;
};

double punto_distancia_impl(const Punto* self) {
    return sqrt((double)self->x * self->x + (double)self->y * self->y);
}

static const PuntoVTable PUNTO_VTBL = {
    .distancia_origen = punto_distancia_impl
};

void punto_init(Punto* p, int x, int y) {
    p->x = x; p->y = y; p->vptr = &PUNTO_VTBL;
}

int main(void) {
    Punto p; punto_init(&p, 3, 4);
    double d = p.vptr->distancia_origen(&p);  /* self == 'this' explícito */
    return 0;
}
```

Aquí estás **simulando métodos y despacho** (y esto te prepara mentalmente para entender **polimorfismo** en C++).

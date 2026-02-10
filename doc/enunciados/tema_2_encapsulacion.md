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
# TEMA 2. Encapsulación

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.

### Respuesta
En **Programación Orientada a Objetos (POO)**, tanto la **encapsulación** como la **ocultación de información** buscan mejorar la seguridad, claridad y mantenibilidad del código, pero no son exactamente lo mismo.

***

## 🔒 Encapsulación

La **encapsulación** consiste en agrupar datos (atributos) y operaciones (métodos) dentro de una misma unidad: la clase.  
Su objetivo es **proteger el estado interno del objeto**, controlando cómo se accede y modifica mediante métodos públicos.

***

## 🙈 Ocultación de información

La **ocultación de información** (information hiding) va un paso más allá:  
busca **evitar que el usuario conozca o manipule detalles internos de la implementación**.

Para lograrlo, se emplean modificadores de acceso como `private`, `protected`, etc.

En resumen:

| Concepto                      | ¿Qué busca?                                                         |
| ----------------------------- | ------------------------------------------------------------------- |
| **Encapsulación**             | Agrupar datos y métodos dentro de una clase.                        |
| **Ocultación de información** | Proteger detalles internos para que no sean accesibles desde fuera. |

***

## ✔️ Ventajas de la ocultación de información

Algunas ventajas importantes:

1.  **Mayor seguridad del estado interno del objeto**  
    Evita que partes externas modifiquen atributos de forma directa e incorrecta.

2.  **Reduce errores y efectos secundarios**  
    Al obligar a usar métodos controlados (getters/setters o funciones específicas).

3.  **Permite cambiar la implementación sin afectar al resto del programa**  
    Mientras la interfaz pública no cambie, el interior puede modificarse libremente.

4.  **Mejora la modularidad y facilita el mantenimiento**  
    El código queda más organizado y es más fácil de entender y depurar.

5.  **Evita dependencias innecesarias**  
    Otros módulos solo conocen lo imprescindible, reduciendo acoplamiento.


## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

### Respuesta
En **Programación Orientada a Objetos**, la **interfaz pública** de una clase u objeto es:

## 🧩 ¿Qué es la *interfaz pública*?

Es **el conjunto de métodos y atributos accesibles desde fuera de la clase** (normalmente marcados como `public`).  
La interfaz pública define **cómo** se puede interactuar con el objeto, sin mostrar **cómo** está implementado internamente.

En otras palabras:  
➡️ **Es la “cara externa” del objeto**, lo único que otros módulos, funciones o clases necesitan conocer para usarlo.

Ejemplo en C++:

```cpp
class CuentaBancaria {
public:
    void ingresar(double cantidad);
    void retirar(double cantidad);
    double getSaldo() const;

private:
    double saldo;   // esto NO forma parte de la interfaz pública
};
```

Los métodos `ingresar`, `retirar` y `getSaldo` **sí** forman parte de la interfaz pública.  
El atributo `saldo` **no**, porque está oculto.

***

## 🔐 Relación con la ocultación de información

La relación es directa:

### ✔️ La interfaz pública es lo que se **expone**

### ✔️ La ocultación de información es lo que se **esconde**

Cuando ocultas información (`private`, `protected`), estás impidiendo que el estado interno sea accesible desde fuera.  
Eso obliga a los usuarios del objeto a usar **solo** la interfaz pública.

Así se consigue:

*   Proteger los datos internos.
*   Controlar cómo se modifican.
*   Reducir errores por acceso indebido.
*   Mantener independencia entre **interfaz** e **implementación**.


## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

### Respuesta

## 🎯 ¿Por qué hay que diseñar con cuidado la interfaz pública?

Porque la **interfaz pública es el contrato** entre la clase y el resto del programa.  
Todo lo que otras clases o módulos hagan dependerá de ella.

Si la interfaz pública está mal diseñada:

*   Se vuelve difícil de usar.
*   Permite usos incorrectos del objeto.
*   Genera dependencias fuertes y acoplamiento.
*   Complica la evolución de la clase en el futuro.

***

## 🔧 ¿Es fácil cambiar la interfaz pública?

❌ **No, no es fácil.**  
Una vez publicada y usada en varias partes del programa, **cambiarla rompe código existente**.  
Por eso, cualquier modificación puede requerir:

*   Revisar mucho código.
*   Actualizar llamadas a métodos.
*   Adaptar dependencias.
*   Recompilar y probar de nuevo.

***

En cambio, **la implementación interna sí puede cambiarse libremente**, siempre que la interfaz pública siga siendo la misma. Por eso es tan importante diseñarla bien desde el principio.


## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

### Respuesta

## 🧩 ¿Qué son las *invariantes de clase*?

Las **invariantes de clase** son **condiciones que siempre deben cumplirse** para que un objeto sea válido durante toda su vida, excepto quizá mientras se está ejecutando un método.

En otras palabras:  
➡️ **Normas internas que garantizan que el objeto está en un estado coherente.**

Ejemplos típicos:

*   En una cuenta bancaria: el saldo **nunca puede ser negativo**.
*   En una fecha: el mes debe estar entre **1 y 12**.
*   En un vector: el tamaño debe ser **≥ 0** y coherente con la memoria asignada.

Estas invariantes deben cumplirse:

*   **Después del constructor**,
*   **Antes y después de cada método público**,
*   **Durante toda la vida del objeto**, salvo procesos internos momentáneos.

***

## 🔐 ¿Por qué la ocultación de información nos ayuda?

La ocultación de información facilita mantener invariantes porque:

1.  **Protege los atributos internos**  
    Si los datos son `private`, el exterior no puede romper las invariantes modificándolos de cualquier forma.

2.  **Obliga a usar métodos controlados**  
    El programador debe usar la **interfaz pública**, donde tú puedes validar los datos y garantizar las invariantes.

3.  **Permite modificar la implementación sin romper las reglas**  
    Puedes reescribir la lógica interna mientras mantengas las invariantes y la interfaz pública siga igual.

4.  **Reduce errores y estados ilegales**  
    Si fuera posible cambiar atributos libremente, sería muy fácil violar condiciones internas.

***

## En resumen

**Invariantes de clase:**  
→ Reglas internas que siempre deben ser ciertas.

**Ocultación de información:**  
→ Evita que alguien desde fuera pueda romper esas reglas.


## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

### Respuesta
¡Vamos a ello, Alonso! Te dejo un ejemplo claro en **Java**, usando **ocultación de información** y respondiendo a tus preguntas.

***

## Clase `Punto` en Java (con ocultación de información)

```java
public class Punto {
    // Atributos ocultos (no accesibles desde fuera de la clase)
    private double x;
    private double y;

    // Constructor: inicializa el estado cumpliendo invariantes si las hubiese
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    // Getters (parte de la interfaz pública)
    public double getX() { 
        return x; 
    }

    public double getY() { 
        return y; 
    }

    // Setters (permiten controlar cambios y validar si hiciera falta)
    public void setX(double x) { 
        this.x = x; 
    }

    public void setY(double y) { 
        this.y = y; 
    }

    // Método público que calcula la distancia al origen (0,0)
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    // (Opcional) método de utilidad: mover el punto
    public void mover(double dx, double dy) {
        this.x += dx;
        this.y += dy;
    }

    // (Opcional) representación en texto
    @Override
    public String toString() {
        return "Punto(" + x + ", " + y + ")";
    }
}
```

### ¿Cómo aplica la ocultación de información aquí?

*   Los atributos `x` e `y` son **`private`**, por lo que **no se pueden tocar directamente desde fuera**.
*   Cualquier acceso o modificación **pasa por métodos públicos** (`getX`, `setX`, etc.), donde podrías **validar** o **proteger invariantes** si las hubiese (por ejemplo, restringir valores).

***

## ¿Cuál es la **interfaz pública** de la clase `Punto`?

La **interfaz pública** es **todo lo accesible desde fuera** de la clase:

*   El **constructor**: `public Punto(double x, double y)`
*   Los **métodos públicos**:
    *   `public double getX()`
    *   `public double getY()`
    *   `public void setX(double x)`
    *   `public void setY(double y)`
    *   `public double calcularDistanciaAOrigen()`
    *   `public void mover(double dx, double dy)` *(si lo incluyes)*
    *   `public String toString()` *(heredado de `Object`, aquí sobrescrito)*

> Nota: Los **atributos `x` e `y` NO forman parte de la interfaz pública** porque son `private`.

***

## ¿Qué significan `public` y `private`?

*   **`public`**:  
    El **miembro es accesible desde cualquier otra clase**.  
    Lo usas para **definir la interfaz pública** (lo que expones al exterior).

*   **`private`**:  
    El **miembro solo es accesible dentro de la propia clase**.  
    Lo usas para **ocultar los detalles internos** (ocultación de información), protegiendo el estado y evitando usos indebidos.

***

## Variante inmutable (opcional y elegante)

Si quieres maximizar la seguridad de estado, puedes hacer la clase **inmutable** (sin setters):

```java
public class Punto {
    private final double x;
    private final double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double getX() { return x; }
    public double getY() { return y; }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    // En vez de modificar, devuelve un nuevo Punto
    public Punto mover(double dx, double dy) {
        return new Punto(this.x + dx, this.y + dy);
    }

    @Override
    public String toString() {
        return "Punto(" + x + ", " + y + ")";
    }
}
```

Aquí, la ocultación de información se complementa con **inmutabilidad**, lo que facilita mantener **invariantes de clase**.

## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

### Respuesta
En **Java**, los modificadores de acceso `public` y `private` se pueden aplicar a distintos elementos del lenguaje, pero **no a todos**. Aquí va una respuesta clara y breve:

***

# ✔️ ¿A quiénes se pueden aplicar `public` o `private` en Java?

## ✅ `public` y `private` se pueden aplicar a:

### **1. Clases (solo de nivel superior o *top-level*)**

*   `public` → **Sí**
*   `private` → **No**, **NO** se puede usar en clases de nivel superior.

Ejemplo válido:

```java
public class MiClase { ... }
```

Ejemplo inválido:

```java
private class MiClase { ... } // ❌ Error
```

### **2. Clases internas (clases dentro de otra clase)**

Para **clases internas**, sí se permiten ambos:

*   `public`
*   `private`

```java
public class A {
    private class B { ... }  // ✔️ clase interna privada
}
```

### **3. Atributos (variables de instancia y de clase)**

Se pueden modificar con:

*   `public`
*   `private`

```java
private int contador;
public String nombre;
```

### **4. Métodos**

También aceptan:

*   `public`
*   `private`

```java
public void mostrar() { ... }
private void comprobar() { ... }
```

### **5. Constructores**

Pueden ser:

*   `public`
*   `private` (muy usado en patrones como *Singleton*)

```java
private MiClase() { }
```

***

# ❌ ¿Dónde NO se pueden usar?

## ❌ No se pueden usar en:

*   **Interfaces (de nivel superior)** con `private`  
    (aunque sí pueden tener métodos privados desde Java 9).
*   **Variables locales** (dentro de métodos)  
    → No aceptan ningún modificador de acceso.
*   **Parámetros de métodos**
*   **Bloques de código**

```java
public void metodo() {
    private int x = 5;  // ❌ Error
}
```

## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

### Respuesta

# 🌐 1. En POO (teóricamente): más tipos de visibilidad

En la teoría general de la Programación Orientada a Objetos, suelen considerarse **tres** niveles de visibilidad:

1.  **Pública** → accesible desde cualquier parte.
2.  **Privada** → accesible solo desde dentro del propio objeto/clase.
3.  **Protegida** (*protected*) → accesible solo por la clase y sus clases derivadas (subclases).

Muchos lenguajes añaden más matices.

***

# ☕ 2. ¿Qué ocurre en *Java*?

Java tiene **4 niveles de visibilidad**:

## ✔️ `public`

Accesible desde cualquier lugar.

## ✔️ `private`

Accesible solo desde la clase que lo define.

## ✔️ `protected`

Accesible desde:

*   la clase que lo define,
*   sus subclases,
*   otras clases del **mismo paquete**.

## ✔️ *package-private* (sin escribir nada)

Este es el “nivel por defecto” en Java.  
Accesible solo desde clases **del mismo paquete**.

Ejemplo:

```java
class Ejemplo {  // package-private, porque no pongo public
    int x;       // package-private
    public int y;
    private int z;
    protected int w;
}
```

Así que Java realmente tiene **4 niveles de visibilidad**, no solo dos.

***

# 🧰 3. ¿Y en otros lenguajes?

Cada lenguaje lo organiza de forma distinta:

## **C++**

Visibilidad para miembros:

*   `public`
*   `protected`
*   `private`

Además, para clases base (`class Base : public A`, `protected`, `private`), la visibilidad cambia la herencia, cosa que no ocurre en Java.

## **Python**

No tiene modificadores reales.  
Usa **convenciones**, no reglas estrictas:

*   `_atributo` → “protegido” (convención)
*   `__atributo` → *name mangling*, oculta parcialmente
*   Todo es accesible realmente, solo se **sugiere**.

## **C#**

Ofrece más visibilidad que Java:

*   `public`
*   `private`
*   `protected`
*   `internal`
*   `protected internal`
*   `private protected`

## **Swift**

Tiene:

*   `private`
*   `fileprivate`
*   `internal`
*   `public`
*   `open`

## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### Respuesta
**Respuesta corta:**  
En **Java**, los miembros de instancia `private` están **ocultos para otras clases** (a), **pero no para otras instancias de la misma clase** (b).  
La **visibilidad es por *clase*, no por *instancia***: cualquier método de la clase puede acceder a los `private` de *cualquier objeto* de esa misma clase.

***

## Ejemplo en Java con `calcularDistanciaAPunto(Punto otro)`

```java
public class Punto {
    // Atributos ocultos al exterior (otras clases no pueden accederlos directamente)
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }

    // Nuevo: distancia entre este punto y otro punto
    public double calcularDistanciaAPunto(Punto otro) {
        // Aquí accedemos a 'otro.x' y 'otro.y' aunque son private.
        // Es válido porque ESTAMOS DENTRO de la clase Punto.
        double dx = this.x - otro.x;
        double dy = this.y - otro.y;
        return Math.sqrt(dx * dx + dy * dy);
    }

    // Getters públicos (opcional)
    public double getX() { return x; }
    public double getY() { return y; }

    @Override
    public String toString() {
        return "Punto(" + x + ", " + y + ")";
    }
}
```

### ¿Qué demuestra este ejemplo?

*   Desde **fuera** de `Punto` (otra clase), **no** puedes hacer `p.x` o `p.y` porque son `private`.
*   **Dentro** de la clase `Punto`, **sí** puedes acceder a los atributos privados de **cualquier objeto `Punto`**, incluido el parámetro `otro`.  
    Por eso `calcularDistanciaAPunto` puede leer `otro.x` y `otro.y`.

***

## Conclusión

*   **(a) Otras clases:** **No** pueden acceder a miembros `private` → **ocultos**.
*   **(b) Otras instancias de la misma clase:** **Sí** son accesibles **desde métodos de la clase** → **no están ocultos entre instancias**.

Esto es clave para implementar operaciones que comparan o combinan objetos del mismo tipo (distancias, equals, compareTo, copy, etc.) sin exponer su estado interno al exterior.


## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

### Respuesta
Los **métodos *getter* y *setter*** son dos tipos de métodos muy comunes en los lenguajes orientados a objetos. Se usan para **acceder** y **modificar** atributos privados respetando el principio de **ocultación de información**.

***

# ✔️ ¿Qué es un *getter*?

Un **getter** es un método **público** que permite **leer** el valor de un atributo privado.

*   Sigue la convención: `getNombreAtributo()`
*   No modifica el estado del objeto

Ejemplo en Java:

```java
public double getX() {
    return x;
}
```

***

# ✔️ ¿Qué es un *setter*?

Un **setter** es un método **público** que permite **asignar** un nuevo valor a un atributo privado.

*   Sigue la convención: `setNombreAtributo(valor)`
*   Puede incluir validaciones para mantener invariantes

Ejemplo:

```java
public void setX(double x) {
    this.x = x;
}
```

***

# 🎯 ¿Para qué sirven?

### 1. **Ocultan los detalles internos**

Los atributos suelen ser `private`; los getters y setters controlan el acceso.

### 2. **Permiten validar valores**

Por ejemplo, impedir valores negativos, rangos incorrectos, etc.

### 3. **Mantienen invariantes de clase**

Aseguran que el objeto nunca entre en un estado inválido.

### 4. **Permiten cambiar la implementación interna sin romper código externo**

Mientras los métodos públicos no cambien, el interior puede reescribirse libremente.

***

# 📌 Resumen en una frase

> Los getters permiten **leer** atributos privados y los setters permiten **modificarlos**, respetando la **encapsulación** y la **ocultación de información** en POO.

## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

### Respuesta
No, **cuando en POO decimos que la ocultación de información mejora la “seguridad” NO nos referimos a la seguridad informática o a evitar que te hackeen**.

Aquí “seguridad” tiene otro significado, más cercano a *robustez* o *correcto funcionamiento interno* del programa.

***

# ✔️ Entonces, ¿qué significa “seguridad” en este contexto?

En **programación orientada a objetos**, la *ocultación de información* mejora la seguridad en el sentido de:

### → **Proteger el estado interno del objeto para que no pueda ser usado de forma incorrecta.**

No significa defenderse de hackers, sino **evitar que el propio programa se rompa** por accesos indebidos a atributos o violaciones de invariantes.

Ejemplos de esta “seguridad”:

*   Que no se pueda poner el saldo de una cuenta bancaria a un valor absurdo directamente.
*   Que no se pueda modificar un atributo de forma que deje al objeto en un estado inválido.
*   Que las actualizaciones al estado se hagan de forma controlada mediante métodos.

***

# ❌ Entonces… ¿evita que alguien pueda hackear mi programa?

**No.**  
Los modificadores `private`, `protected` o `public` **no protegen contra ataques externos**.

Son herramientas del lenguaje destinadas a:

*   la **organización interna del programa**,
*   la **corrección**,
*   la **mantenibilidad**,
*   y la **prevención de errores lógicos**.

Un atacante real no se detiene por un `private`.

***

# ✔️ Resumen breve

*   **“Seguridad” en POO →** seguridad *lógica* del programa (evitar usos incorrectos, mantener invariantes).
*   **NO es seguridad informática →** no evita hackeos, no protege frente a ataques, no cifra nada.
*   Ocultar información sirve para que **los objetos solo se usen como deben usarse**.

## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

### Respuesta
Aquí tienes una explicación clara y directa, sin necesidad de búsquedas porque es contenido teórico de programación orientada a objetos.

***

# 🔹 Diferencia entre **miembro de instancia** y **miembro de clase**

## ✔️ **Miembro de instancia**

Es un atributo o método cuyo valor **pertenece a cada objeto individual**.

*   Cada instancia (cada objeto creado con `new`) tiene **su propia copia** del atributo.
*   Se accede mediante un objeto: `p.x`.

Ejemplo en Java:

```java
public class Punto {
    private double x; // miembro de instancia
    private double y; // miembro de instancia
}
```

Si creas dos objetos:

```java
Punto p1 = new Punto(1, 2);
Punto p2 = new Punto(5, 8);
```

`p1.x` y `p2.x` son **distintos valores**, almacenados por separado.

***

## ✔️ **Miembro de clase**

Es un atributo o método compartido por **todas las instancias** de la clase.

*   Se declara con la palabra clave **`static`**.
*   Solo existe **una única copia**, independientemente del número de objetos.
*   Se accede mediante el nombre de la clase: `Punto.contador`.

Ejemplo:

```java
public class Punto {
    private static int contador = 0; // miembro de clase

    public Punto(double x, double y) {
        contador++; // aumenta el total de puntos creados
    }
}
```

Todos los objetos comparten el mismo `contador`.

***

# 🔹 ¿Se pueden ocultar los miembros de clase?

### ✔️ Sí, también se pueden ocultar.

Un miembro de clase (`static`) puede ser:

*   `public`
*   `private`
*   `protected`
*   package-private (sin modificador)

Ejemplo:

```java
public class Punto {
    private static int contador = 0;  // oculto
    private double x;
    private double y;

    public static int getContador() { // parte pública
        return contador;
    }
}
```

El atributo estático `contador` es `private`, por lo que:

*   **Otras clases NO pueden acceder directamente a él** (`Punto.contador` es ilegal).
*   Solo está accesible desde **métodos de la clase**, igual que un atributo no estático privado.


# 🧠 Idea clave

> La ocultación de información funciona **igual** para miembros de instancia y de clase:  
> si los declaras `private`, están ocultos a otras clases.


## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Respuesta
Sí, **tiene sentido que los constructores sean privados**, aunque solo en casos muy concretos.

### ✔️ ¿Cuándo tiene sentido un constructor `private`?

1.  **Para impedir que otros creen objetos libremente**  
    Se usa cuando quieres **controlar totalmente** cómo y cuándo se crean las instancias.

2.  **En el patrón *Singleton***  
    La clase solo puede tener **una única instancia**.  
    El constructor privado impide crear más objetos desde fuera.

3.  **En clases con métodos de fábrica (*factory methods*)**  
    La clase no permite crear objetos con `new`; obliga a usar métodos como:
    ```java
    public static Punto crearDesdePolar(double r, double theta)
    ```
    Así puedes validar entradas o decidir qué tipo exacto de objeto devolver.

4.  **Para crear clases inmutables con control de construcción**  
    A veces se oculta el constructor y se ofrece un *builder* o métodos estáticos.

***

### ✔️ Idea clave

> Un constructor privado **no impide crear objetos**, sino que **limita quién puede crearlos**.  
> La propia clase sí puede crear instancias (por ejemplo, dentro de un método estático).


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Respuesta

## ¿Cómo se indican los **miembros de clase** en Java?

Los **miembros de clase** se declaran con la palabra clave **`static`**.

*   **Atributos `static`** → una **única copia compartida** por **todas** las instancias.
*   **Métodos `static`** → se invocan con el **nombre de la clase**, no con un objeto.

***

## Ejemplo: `Punto` con máximos globales de `x` e `y`

Objetivo: guardar, de forma **global** a la clase, los valores máximos de `x` e `y` que se hayan establecido en **cualquier** objeto `Punto` creado hasta el momento.

### Versión **mutable** (con setters)

```java
public class Punto {
    // Miembros de instancia (propios de cada objeto)
    private double x;
    private double y;

    // Miembros de clase (compartidos por todos los objetos)
    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    // Constructor
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
        actualizarMaximos(x, y); // actualiza los máximos globales
    }

    // Getters de instancia
    public double getX() { return x; }
    public double getY() { return y; }

    // Setters de instancia (si se modifica el punto, también actualizamos)
    public void setX(double x) {
        this.x = x;
        actualizarMaximos(this.x, this.y);
    }

    public void setY(double y) {
        this.y = y;
        actualizarMaximos(this.x, this.y);
    }

    // Método de instancia de utilidad
    public double calcularDistanciaAOrigen() {
        return Math.hypot(x, y);
    }

    // ---- Miembros de clase públicos para consultar los máximos ----
    public static double getMaxX() { return maxX; }
    public static double getMaxY() { return maxY; }

    // ---- Lógica interna (privada) para mantener los máximos ----
    private static void actualizarMaximos(double x, double y) {
        if (x > maxX) maxX = x;
        if (y > maxY) maxY = y;
    }

    @Override
    public String toString() {
        return "Punto(" + x + ", " + y + ")";
    }
}
```

**Uso:**

```java
Punto a = new Punto(1.5, 3.0);
Punto b = new Punto(2.0, -4.0);
b.setY(5.5);

System.out.println(Punto.getMaxX()); // 2.0
System.out.println(Punto.getMaxY()); // 5.5
```

### Variante **inmutable** (sin setters)

Si prefieres inmutabilidad (más segura para invariantes), actualizas los máximos **solo** en el constructor y en métodos que crean **nuevos puntos**:

```java
public class Punto {
    private final double x;
    private final double y;

    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
        actualizarMaximos(x, y);
    }

    public double getX() { return x; }
    public double getY() { return y; }

    public double calcularDistanciaAOrigen() {
        return Math.hypot(x, y);
    }

    // Devuelve un nuevo Punto desplazado
    public Punto mover(double dx, double dy) {
        return new Punto(this.x + dx, this.y + dy);
    }

    public static double getMaxX() { return maxX; }
    public static double getMaxY() { return maxY; }

    private static void actualizarMaximos(double x, double y) {
        if (x > maxX) maxX = x;
        if (y > maxY) maxY = y;
    }

    @Override
    public String toString() {
        return "Punto(" + x + ", " + y + ")";
    }
}
```

***

## Puntos clave

*   **`static`** indica **miembro de clase** (compartido), accesible como `Punto.getMaxX()`.
*   Los máximos se **ocultan** (`private static`) y se exponen con **getters estáticos**.
*   Si la clase es **mutable**, recuerda actualizar los máximos también en los **setters**.
*   (Avanzado) En contextos **multihilo**, la actualización de máximos debería protegerse (por ejemplo, con `synchronized` o `AtomicDouble`/bloqueo), pero para ejercicios introductorios no suele pedirse.

## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

### Respuesta
Sí: **debe ser `static`**, porque un método factoría pertenece a la **clase**, no a una instancia concreta.

```java
public static Punto crearRedondeado(double x, double y) {
    int rx = (int) Math.round(x);
    int ry = (int) Math.round(y);
    return new Punto(rx, ry);
}
```

### Explicación breve

*   Es **método de clase** (`static`) → lo llamas como `Punto.crearRedondeado(...)`.
*   Usa `Math.round()` para redondear.
*   Devuelve un **nuevo objeto `Punto`** ya redondeado.

## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

### Respuesta

> Detalles de diseño:
>
> *   El array `xy` es `final` (la **referencia** no cambia), pero sus valores sí pueden cambiar (clase **mutable**).
> *   No se expone el array; solo se accede mediante getters/setters y métodos públicos.
> *   Incluyo el método factoría `crearRedondeado` que pediste antes.

```java
public class Punto {
    // Representación interna: array de dos posiciones [x, y]
    private final double[] xy; // xy[0] = x, xy[1] = y

    // ---- Constructores ----
    public Punto(double x, double y) {
        this.xy = new double[] { x, y };
    }

    // ---- Getters (interfaz pública previamente definida) ----
    public double getX() { return xy[0]; }
    public double getY() { return xy[1]; }

    // ---- Setters (mantienen la interfaz pública) ----
    public void setX(double x) { xy[0] = x; }
    public void setY(double y) { xy[1] = y; }

    // ---- Lógica de dominio ----
    public double calcularDistanciaAOrigen() {
        // Math.hypot es estable y claro para sqrt(x^2 + y^2)
        return Math.hypot(xy[0], xy[1]);
    }

    public double calcularDistanciaAPunto(Punto otro) {
        // Acceso permitido: estamos dentro de la misma clase Punto
        double dx = this.xy[0] - otro.xy[0];
        double dy = this.xy[1] - otro.xy[1];
        return Math.hypot(dx, dy);
    }

    // Desplaza el punto (versión mutable, mantiene firma previa)
    public void mover(double dx, double dy) {
        xy[0] += dx;
        xy[1] += dy;
    }

    // Método factoría pedido anteriormente (estático)
    public static Punto crearRedondeado(double x, double y) {
        int rx = (int) Math.round(x);
        int ry = (int) Math.round(y);
        return new Punto(rx, ry);
    }

    @Override
    public String toString() {
        return "Punto(" + xy[0] + ", " + xy[1] + ")";
    }
}
```

### Notas rápidas

*   **Interfaz pública preservada**: `getX`, `getY`, `setX`, `setY`, `calcularDistanciaAOrigen`, `calcularDistanciaAPunto`, `mover`, `toString`, y el *factory method* `crearRedondeado` se mantienen con las mismas **firmas**.
*   Solo cambia la **representación interna**: ahora es un `double[]` en lugar de dos `double`. Esto ilustra la independencia entre **interfaz** e **implementación**, gracias a la **ocultación de información**.

## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Respuesta
Vamos por partes, Alonso —respuesta **breve, clara y directa**, como pides, y totalmente teórica (no requiere búsquedas).

***

# 🧩 1. Si un atributo tiene *getter* y *setter* públicos, ¿no sería mejor declararlo público?

**No.**  
Aunque un atributo tenga *getter* y *setter*, **no debe declararse público**.

¿Por qué?

### ✔️ Porque el atributo forma parte de la **implementación interna**

Si lo declaras público:

*   ya no tienes control sobre cómo se accede o modifica,
*   no puedes validar nada,
*   rompes la ocultación de información,
*   y acoplas fuertemente tu clase al exterior.

En cambio, si usas *getter* y *setter*:

*   puedes añadir validaciones en el futuro,
*   puedes cambiar la representación interna sin romper código externo,
*   puedes proteger invariantes.

***

# 🧩 2. ¿Cuál es la convención más habitual?

La convención universal en POO, especialmente en Java, es:

### ✔️ **Los atributos deben ser privados (`private`)**

### ✔️ **El acceso debe darse mediante getters/setters (si son necesarios)**

Esto aparece en prácticamente todas las guías de estilo de Java (Oracle, comunidad, libros como *Effective Java*).

***

# 🧩 3. ¿Tiene esto algo que ver con las "invariantes de clase"?

**Sí, muchísimo.**  
Declarar los atributos como `private` está directamente relacionado con proteger las invariantes de clase.

### ✔️ Si los atributos son públicos:

*   cualquier parte del programa podría ponerlos en un estado inválido
*   las invariantes pueden romperse fácilmente
*   no tienes forma de interceptar cambios

### ✔️ Si los atributos son privados:

*   solo se pueden modificar mediante métodos controlados (setters u otros)
*   puedes comprobar valores antes de asignarlos
*   puedes garantizar que **las invariantes siempre se mantengan**

***

# 🧠 Resumen final

*   **¿Mejor hacer un atributo público si tiene getters/setters?**  
    ❌ *No.* Siempre debe ser `private`.

*   **¿Convención habitual?**  
    ✔️ Atributos **privados**.  
    ✔️ Acceso a través de métodos públicos (getters/setters).

*   **¿Relación con invariantes de clase?**  
    ✔️ Los atributos privados permiten **proteger las invariantes**, evitando que el objeto entre en estados ilegales.


## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Respuesta
# 🧩 1. ¿Qué significa que una clase sea **inmutable**?

Una clase **inmutable** es aquella cuyo **estado interno no puede cambiar** después de haber sido creada.

En otras palabras:

> Una vez construyes el objeto, **sus atributos nunca cambian**.

Ejemplo típico: `String` en Java es inmutable.

Para que una clase sea inmutable, normalmente se hace:

*   Atributos `private`
*   Atributos `final`
*   Sin setters
*   Métodos “modificadores” que **devuelven un nuevo objeto**, no modifican el actual

***

# 🧩 2. ¿Qué es un **método modificador**?

Un **método modificador** es un método que **cambia el estado interno del objeto**.  
En una clase mutable, cambia atributos; en una inmutable, devuelve un objeto nuevo.

Ejemplos típicos:

*   `setX(double x)`
*   `mover(double dx, double dy)` (si cambia `x` e `y`)

***

# 🧩 3. ¿Un método modificador es siempre un "setter"?

**No.**

Un *setter* es un tipo de método modificador, pero **no el único**.

### Ejemplos de métodos modificadores que **no** son setters:

```java
public void incrementarContador() { contador++; }

public void mover(double dx, double dy) {
    this.x += dx;
    this.y += dy;
}
```

Estos modifican el estado interno, pero **no** son setters.

***

# 🧩 4. ¿Tiene ventajas que una clase sea **inmutable**?

Sí, tiene **muchas ventajas**, especialmente en diseño de software:

## ✔️ 1. Son más fáciles de razonar

Al no cambiar nunca, sabes que un objeto conserva su estado original.

## ✔️ 2. Evitan errores por efectos secundarios

Nadie puede modificar el objeto “por sorpresa”.

## ✔️ 3. Son seguras en entornos multihilo

Como no cambian, no necesitas sincronización.

## ✔️ 4. Facilitan mantener invariantes

Si los atributos no cambian, las invariantes siempre se mantienen una vez creado el objeto.

## ✔️ 5. Se pueden compartir sin miedo

Puedes pasar una referencia a cualquier parte del programa sin preocuparte de que lo modifiquen.

***

# 🧠 Resumen final

*   **Clase inmutable:** su estado no cambia una vez construida.
*   **Método modificador:** cambia el estado del objeto (pero **no** siempre es un setter).
*   **Setter:** un tipo particular de método modificador.
*   **Ventajas de la inmutabilidad:** simplicidad, seguridad, facilidad para mantener invariantes, y seguridad en multihilo.

## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### Respuesta
No, **no es recomendable incluir siempre métodos *setter* como convención**.  
De hecho, en el diseño moderno de POO, **la tendencia es incluir *setters* solo cuando realmente sean necesarios**.

Vamos punto por punto:

***

# ✔️ ¿Se deben incluir *setters* por defecto?

**❌ No.**  
Incluir setters automáticamente es una mala práctica.

¿Por qué?

*   Expone demasiado el estado interno.
*   Reduce la encapsulación y la ocultación de información.
*   Facilita romper invariantes de clase.
*   Hace que la clase sea más difícil de mantener, evolucionar y proteger.

Un *setter* permite modificar un atributo en cualquier momento, lo cual **no siempre es deseable**.

***

# ✔️ ¿Cuál es la convención recomendada?

La convención habitual (especialmente en Java) es:

### 👉 **Atributos privados (`private`) y no añadir setters salvo que hagan falta.**

En otras palabras:

> Si un atributo **no necesita ser modificado desde fuera**, entonces **no debe tener setter**.

Y muy a menudo, muchos atributos **no necesitan setter**.

***

# ✔️ ¿Qué alternativas hay a los setters?

1.  **Clases inmutables**  
    → No tienen setters; solo getters.  
    → Cualquier modificación genera un nuevo objeto.

2.  **Métodos modificadores controlados**  
    → Cambian el estado, pero aplicando una lógica específica.  
    → Ejemplo: `mover(dx, dy)` en vez de `setX()`, `setY()`.

3.  **Setters con validación**  
    → Si se necesitan, pueden asegurar invariantes:
    ```java
    public void setEdad(int edad) {
        if (edad < 0) throw new IllegalArgumentException("Edad negativa");
        this.edad = edad;
    }
    ```

***

# ✔️ ¿Qué relación tiene esto con las invariantes de clase?

Muchísima.

Si permites cambiar atributos libremente mediante setters públicos:

*   Cualquiera puede poner el objeto en un estado **inválido**.
*   Se pueden romper invariantes internas fácilmente.

En cambio:

*   Si controlas o limitas la existencia de setters,
*   puedes **proteger las invariantes** y mantener el objeto siempre en un estado coherente.

***

# 🧠 Resumen final

*   **No**, no es recomendable incluir setters siempre.
*   **Convención:** atributos privados, y setters solo cuando sean necesarios.
*   **Un setter es una puerta para modificar el estado**, así que debe existir solo si el diseño lo pide.
*   **Las invariantes de clase** son más fáciles de mantener si la clase tiene menos setters o es inmutable.

## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### Respuesta

# ✔️ ¿La clase `String` en Java es mutable o inmutable?

**`String` en Java es *inmutable*.**

Esto significa que **una vez creada una cadena, su contenido no puede cambiar**.

***

# ✔️ ¿Qué ocurre al concatenar dos cadenas?

Cuando haces algo como:

```java
String s = "Hola";
s = s + " mundo";
```

NO se modifica la cadena `"Hola"`.

Lo que ocurre es:

1.  Se crea **un nuevo objeto `String`** con el resultado `"Hola mundo"`.
2.  La referencia `s` pasa a apuntar al nuevo objeto.
3.  El objeto antiguo queda sin usar (y lo recolectará el *garbage collector* eventualmente).

Por tanto, **cada concatenación crea un objeto nuevo**, lo cual puede ser *muy ineficiente* si se hace muchas veces.

***

# ✔️ ¿Qué debemos hacer si vamos a concatenar muchas veces?

Usar **`StringBuilder`** (o `StringBuffer` si necesitas sincronización, que no suele ser el caso).

Ejemplo:

```java
StringBuilder sb = new StringBuilder();

for (int i = 0; i < 10000; i++) {
    sb.append("Hola ");
}

String resultado = sb.toString();
```

### ¿Por qué?

*   `StringBuilder` **sí es mutable**.
*   Permite **modificar la cadena internamente sin crear miles de objetos nuevos**.
*   Es mucho más **eficiente** cuando hay concatenaciones dentro de bucles.

***

# 🧠 Resumen final

*   ✔️ `String` en Java es **inmutable**.
*   ✔️ Al concatenar, **se crean nuevos objetos** cada vez.
*   ✔️ Para concatenaciones repetidas o construcción incremental de cadenas largas, usa **`StringBuilder`**.

## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

### Respuesta

# ✔️ En POO ¿cómo se comparan objetos: por contenido o por identidad?

Depende **del lenguaje** y **del método usado**.

En general:

*   **Identidad** → si son *el mismo objeto en memoria*.
*   **Contenido** → si tienen *los mismos valores internos*.

En Java:

*   `==` compara **identidad**.
*   `equals()` compara **contenido** (si la clase está bien diseñada).

***

# ✔️ ¿Qué es el método `equals` en Java?

`equals` es un método heredado de la clase `Object` que sirve para comparar **si dos objetos son “equivalentes” en contenido**.

Firma:

```java
public boolean equals(Object obj)
```

***

# ✔️ ¿Qué hace `equals` por defecto?

Por defecto (`Object.equals`):

> **Hace lo mismo que `==` → compara identidad, no contenido.**

Eso significa que si no sobrescribes `equals`, dos objetos con el mismo contenido se considerarán **distintos**, porque son dos instancias distintas.

Ejemplo:

```java
String a = new String("hola");
String b = new String("hola");

a == b        // false (identidad)
a.equals(b)   // true  (contenido, porque String sobrescribe equals)
```

***

# ✔️ ¿Cómo se deben comparar dos cadenas en Java?

### Nunca con `==`

`==` compara **identidad de referencia**, no contenido.  
Puede dar resultados inconsistentes según vengan del *string pool* o no.

### Siempre con `equals` (o `equalsIgnoreCase`)

Ejemplo:

```java
String s1 = "hola";
String s2 = "hola";

s1.equals(s2);            // true (contenido)
s1 == s2;                 // puede ser true o false, no usar
```

***

# 🧠 Resumen final

*   En POO, los objetos pueden compararse por **identidad** (`==`) o por **contenido** (`equals` en Java).
*   `equals` es el método usado para comparar **contenido lógico**.
*   Por defecto, `equals` en `Object` compara **identidad**, igual que `==`.
*   Para comparar cadenas en Java: **usar `equals`**, nunca `==`.

## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Respuesta

# ✔️ ¿Qué son las clases *wrapper*?

En un lenguaje orientado a objetos como **Java**, las clases *wrapper* son **clases que envuelven (o "empaquetan") valores de tipos primitivos**, permitiendo tratarlos como **objetos**.

Ejemplos en Java:

| Tipo primitivo | Wrapper     |
| -------------- | ----------- |
| `int`          | `Integer`   |
| `double`       | `Double`    |
| `boolean`      | `Boolean`   |
| `char`         | `Character` |
| ...            | ...         |

Se les llama *wrappers* porque **"envuelven"** el valor dentro de un objeto.

***

# ✔️ ¿Para qué sirven?

Los tipos primitivos **no son objetos**, pero muchas estructuras en Java **solo funcionan con objetos**, como:

*   colecciones (`ArrayList`, `HashMap`, …)
*   genéricos
*   métodos que requieren objetos
*   APIs orientadas a objetos en general

Las clases wrapper permiten usar valores primitivos **como objetos** cuando es necesario.

***

# ✔️ ¿Cómo se hace? ¿Es un proceso automático?

En Java:

### ➤ **Autoboxing**

Conversión automática **de primitivo → wrapper**.

```java
Integer x = 5;   // autoboxing
```

Java convierte `5` en `Integer.valueOf(5)`.

***

### ➤ **Unboxing**

Conversión automática **de wrapper → primitivo**.

```java
int y = x;       // unboxing
```

Java convierte `x.intValue()` automáticamente.

**Sí, es un proceso automático** (desde Java 5), aunque también puede hacerse manualmente.

***

# ✔️ ¿Qué ventajas tienen las clases wrapper?

1.  **Permiten almacenar valores primitivos en colecciones**, que solo aceptan objetos:
    ```java
    ArrayList<Integer> lista = new ArrayList<>();
    ```

2.  **Permiten representar “ausencia de valor” con `null`**, cosa que los primitivos no permiten.

3.  **Ofrecen métodos útiles**:
    *   parseo (`Integer.parseInt("42")`)
    *   comparación
    *   conversión
    *   constantes (`Integer.MAX_VALUE`, `Double.NaN`…)

4.  **Integración con las APIs de Java**  
    Muchas bibliotecas esperan objetos, no valores primitivos.

***

# ✔️ ¿Todos los lenguajes OO tienen tipos primitivos y wrappers?

**No.**

Depende del lenguaje:

### ✔️ **Java, C#, Kotlin → Sí tienen primitivos y wrappers.**

Necesitan wrappers porque sus tipos básicos **no son objetos**.

### ✔️ **Python, Ruby, JavaScript → No.**

En estos lenguajes **todo es objeto**, incluso los números o booleanos:

```python
x = 5     # ya es un objeto
```

Por tanto, **no necesitan wrappers**.

***

# 🧠 Resumen final

*   **Clases wrapper:** clases que envuelven tipos primitivos para tratarlos como objetos.
*   **Proceso automático:** en Java, sí (autoboxing y unboxing).
*   **Ventajas:** usar en colecciones, métodos útiles, permitir `null`, integración con APIs.
*   **¿Todos los lenguajes lo necesitan?** No. Algunos lenguajes OO no tienen tipos primitivos.

## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Respuesta

# ✔️ ¿Qué es un **tipo de dato enumerado** en POO?

Un **tipo de dato enumerado** (*enum*) es un tipo cuyos valores posibles están **predefinidos** y forman un conjunto **fijo y cerrado**.

Ejemplos típicos de enumerados:

*   Días de la semana
*   Colores básicos
*   Direcciones (NORTE, SUR, ESTE, OESTE)

Su función principal es **restringir el dominio** de valores posibles y dar **significado** al código.

***

# ✔️ En Java, ¿un tipo enumerado es una clase?

**Sí.**  
En Java, un `enum` es realmente una **clase especial** que:

*   extiende implícitamente `java.lang.Enum`
*   tiene instancias predefinidas (cada valor del enum es un objeto)
*   tiene constructores privados
*   puede tener métodos, atributos, interfaces, etc.

Ejemplo:

```java
public enum Color {
    ROJO, VERDE, AZUL;
}
```

Todos los valores (`ROJO`, `VERDE`, `AZUL`) son **instancias únicas** de la clase `Color`.

***

# ✔️ ¿Qué ventajas tienen los enumerados en términos de encapsulación en Java?

Los `enum` en Java aportan varias ventajas importantes para la **encapsulación** y la **seguridad del diseño**:

***

## ✔️ 1. **Conjunto cerrado de valores**

Un `enum` define *exactamente* los valores posibles.

*   No puede crearse un valor inválido.
*   Evita errores como usar constantes sueltas, integers mágicos, o strings mal escritos.

Esto protege **invariantes de clase** y evita usos incorrectos.

***

## ✔️ 2. **Instancias controladas**

Las instancias se crean **solo dentro del propio enum**, nunca desde fuera.

*   El constructor es siempre **privado**.
*   No existe `new Color(...)`.

Esto es pura **ocultación de información**:  
el exterior no puede “romper” el enum creando valores no permitidos.

***

## ✔️ 3. **Pueden tener métodos y atributos privados**

Un enum puede encapsular comportamiento:

```java
public enum Dia {
    LUNES(true),
    SABADO(false);

    private final boolean laborable;

    Dia(boolean laborable) { this.laborable = laborable; }

    public boolean esLaborable() { return laborable; }
}
```

Aquí:

*   El atributo `laborable` está **oculto**, es `private`.
*   Se accede mediante un método público.
*   La implementación interna puede cambiar sin afectar al exterior.

***

## ✔️ 4. **Seguridad en la comparación**

Comparar enums con `==` es seguro (identidad y contenido coinciden).  
Esto evita muchos errores típicos con cadenas o enteros.

***

# 🧠 Resumen final

*   Un **tipo enumerado** define un conjunto fijo de valores posibles.
*   En Java, los `enum` **son clases especiales** con instancias predeterminadas.
*   Los enumerados **mejoran la encapsulación** porque:
    *   restringen el dominio de valores,
    *   protegen las invariantes,
    *   ocultan detalles internos,
    *   controlan completamente la creación de instancias,
    *   permiten añadir comportamiento de forma segura.

## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.

### Respuesta
Aquí tienes un **tipo enumerado `Mes` en Java** con las **doce instancias**, que encapsula sus datos con **atributos privados**, **constructor privado**, y proporciona métodos para:

*   **`dias()`** → cuántos días tiene el mes en año no bisiesto.
*   **`dias(int anio)`** → cuántos días tiene el mes teniendo en cuenta si el año es bisiesto (opcional pero útil).
*   **`ordinalMes()`** → ordinal del mes en el año (1–12).

```java
public enum Mes {
    ENERO(1, 31),
    FEBRERO(2, 28), // 29 en bisiestos (ver método dias(int))
    MARZO(3, 31),
    ABRIL(4, 30),
    MAYO(5, 31),
    JUNIO(6, 30),
    JULIO(7, 31),
    AGOSTO(8, 31),
    SEPTIEMBRE(9, 30),
    OCTUBRE(10, 31),
    NOVIEMBRE(11, 30),
    DICIEMBRE(12, 31);

    // Atributos privados (encapsulación)
    private final int ordinalMes;       // 1..12
    private final int diasNoBisiesto;   // Días en año no bisiesto

    // Constructor privado (siempre es privado en enums)
    Mes(int ordinalMes, int diasNoBisiesto) {
        this.ordinalMes = ordinalMes;
        this.diasNoBisiesto = diasNoBisiesto;
    }

    /** Ordinal del mes en el año (1–12). */
    public int ordinalMes() {
        return ordinalMes;
    }

    /** Días del mes en un año no bisiesto. */
    public int dias() {
        return diasNoBisiesto;
    }

    /** Días del mes considerando si el año es bisiesto (solo afecta a FEBRERO). */
    public int dias(int anio) {
        if (this == FEBRERO && esBisiesto(anio)) {
            return 29;
        }
        return diasNoBisiesto;
    }

    // Implementación interna (oculta) de la lógica de año bisiesto.
    private static boolean esBisiesto(int anio) {
        // Regla gregoriana: divisible por 4, excepto siglos no divisibles por 400.
        return (anio % 4 == 0) && ((anio % 100 != 0) || (anio % 400 == 0));
    }
}
```

> **Notas de diseño**
>
> *   El enum es una **clase especial**: las instancias (`ENERO`, `FEBRERO`, …) son objetos únicos.
> *   Los **atributos son privados** y se inicializan vía **constructor**.
> *   Se expone una **interfaz pública clara** (`ordinalMes`, `dias`, `dias(int)`), manteniendo la implementación (como `esBisiesto`) **oculta**.


## 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### Respuesta

```java
// --- Añadir dentro del enum Mes ---

public boolean esDePrimavera(boolean esHemisferioNorte) {
    return esHemisferioNorte
            ? esUnoDe(MARZO, ABRIL, MAYO)
            : esUnoDe(SEPTIEMBRE, OCTUBRE, NOVIEMBRE);
}

public boolean esDeVerano(boolean esHemisferioNorte) {
    return esHemisferioNorte
            ? esUnoDe(JUNIO, JULIO, AGOSTO)
            : esUnoDe(DICIEMBRE, ENERO, FEBRERO);
}

public boolean esDeOtoño(boolean esHemisferioNorte) {
    return esHemisferioNorte
            ? esUnoDe(SEPTIEMBRE, OCTUBRE, NOVIEMBRE)
            : esUnoDe(MARZO, ABRIL, MAYO);
}

public boolean esDeInvierno(boolean esHemisferioNorte) {
    return esHemisferioNorte
            ? esUnoDe(DICIEMBRE, ENERO, FEBRERO)
            : esUnoDe(JUNIO, JULIO, AGOSTO);
}

// Auxiliar privado para comprobar pertenencia a un conjunto de meses
private boolean esUnoDe(Mes... meses) {
    for (Mes m : meses) {
        if (this == m) return true;
    }
    return false;
}
```

**Criterio usado (hemisferio norte):**

*   **Invierno:** diciembre–enero–febrero
*   **Primavera:** marzo–abril–mayo
*   **Verano:** junio–julio–agosto
*   **Otoño:** septiembre–octubre–noviembre

En el **hemisferio sur** se invierten las estaciones.

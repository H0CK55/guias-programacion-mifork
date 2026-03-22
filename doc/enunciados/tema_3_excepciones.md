<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Excepciones". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.

### Respuesta

# ✅ **1. Cómo indicar un error desde una función en C (sin excepciones)**

En C no existe un mecanismo de excepciones, de modo que los errores deben comunicarse manualmente. Cuando una función como `raiz()` necesita informar de un fallo ―por ejemplo, recibir un número negativo― debe devolver algún tipo de indicador que permita al código que la llama detectar el problema. Esta separación entre “lógica de cálculo” y “gestión del error” requiere diseñar previamente cómo va a comunicarse esa información.

Existen varias formas de hacerlo, y elegir una u otra depende del estilo del programa y del tipo de datos que maneje la función. A continuación se presentan **dos opciones clásicas** muy utilizadas en programación en C.

***

## ✅ **Opción 1 — Devolver un valor especial de error (por ejemplo: `-1`)**

Una estrategia simple consiste en que la función devuelva un **valor imposible** o reservado exclusivamente para indicar error. En el caso de una raíz cuadrada, el resultado válido siempre es **≥ 0**, así que se puede usar `-1` como valor especial. El código que llama a la función comprueba si el retorno es ese valor y, si lo es, informa al usuario desde fuera de `raiz()`.

Este método es sencillo y no requiere estructuras adicionales, pero tiene la limitación de que **no siempre existe un valor no ambiguo** para representar el error, especialmente cuando la función ya puede devolver cualquier número válido dentro de un rango amplio.

```c
#include <stdio.h>
#include <math.h>

float raiz(float x) {
    if (x < 0) {
        return -1;    // valor especial indicando error
    }
    return sqrtf(x);
}

int main() {
    float n = -9;
    float r = raiz(n);

    if (r == -1) {
        printf("Error: no se puede calcular la raiz de un número negativo.\n");
    } else {
        printf("La raiz es: %.2f\n", r);
    }

    return 0;
}
```

***

## ✅ **Opción 2 — Usar un parámetro de salida para indicar error (bandera)**

Otra forma común consiste en que la función devuelva el resultado con normalidad, pero reciba además un **puntero a una variable donde escribir un código de error**. La función puede devolver el valor calculado, pero usa ese parámetro adicional para decir si la operación ha sido correcta. De este modo se separan claramente los datos matemáticos del estado del error.

Este enfoque resulta más robusto que devolver un valor especial, porque permite distinguir de forma inequívoca entre el resultado real y la presencia de un error. Además, se pueden definir distintos códigos de error si fuera necesario, mejorando la flexibilidad de la función.

```c
#include <stdio.h>
#include <math.h>

float raiz(float x, int *error) {
    if (x < 0) {
        *error = 1;     // 1 indica error
        return 0;       // valor no significativo
    }
    *error = 0;         // 0 indica éxito
    return sqrtf(x);
}

int main() {
    int err;
    float n = -9;
    float r = raiz(n, &err);

    if (err) {
        printf("Error: número negativo.\n");
    } else {
        printf("La raiz es: %.2f\n", r);
    }

    return 0;
}



## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?

### Respuesta

Una **excepción** es un objeto especial que representa una situación anómala o inesperada que ocurre durante la ejecución de un programa. Su aparición indica que una operación no ha podido completarse correctamente, como leer un archivo inexistente, dividir entre cero o acceder fuera de un rango permitido. A diferencia de un simple código de error en C, una excepción permite interrumpir automáticamente el flujo normal del programa y delegar el manejo del problema a un bloque específico (`catch`), proporcionando así una estructura clara y organizada para tratar fallos.

El objetivo principal de usar excepciones es **separar la lógica normal del programa del manejo de errores**, evitando que el código principal quede lleno de comprobaciones manuales. Cuando un programador implementa una función, puede lanzar una excepción para indicar que no puede continuar y que el error debe gestionarse desde un nivel superior. Del mismo modo, quien llama a esa función puede decidir capturar esa excepción para informar al usuario, recuperar el estado del programa o realizar acciones correctivas. Este mecanismo permite escribir código más limpio, modular y fácil de mantener, especialmente en sistemas complejos.


## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

### Respuesta

A continuación se muestra el ejemplo de la raíz reescrito en Java usando una clase `Calculadora`. En Java, cuando se recibe un dato inválido, en lugar de devolver un valor especial como en C, es habitual **lanzar una excepción**. De esta forma, la función indica que no puede continuar con la operación, y la gestión del error se realiza desde el exterior, normalmente en el método `main` u otro nivel superior. Este enfoque permite separar claramente la lógica de cálculo del tratamiento del error, consiguiendo un código más legible y mantenible.

El método `raiz` lanzará una `IllegalArgumentException` si se intenta calcular la raíz de un número negativo. Desde el `main`, se utilizará un bloque `try–catch` para capturar la excepción y mostrar un mensaje al usuario sin que el programa termine de forma abrupta. Este patrón es muy común en Java y representa la forma más elegante de notificar errores en tiempo de ejecución.

***

# ✔️ Código de ejemplo en Java

```java
public class Calculadora {

    public static double raiz(double x) {
        if (x < 0) {
            throw new IllegalArgumentException("No se puede calcular la raíz de un número negativo");
        }
        return Math.sqrt(x);
    }

    public static void main(String[] args) {
        try {
            double r = Calculadora.raiz(-9);   // prueba de número negativo
            System.out.println("La raíz es: " + r);
        } catch (IllegalArgumentException e) {
            System.out.println("Error capturado desde fuera: " + e.getMessage());
        }

        System.out.println("El programa continúa ejecutándose normalmente.");
    }
}
```

## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.

### Respuesta

Lanzar una excepción consiste en crear un objeto de tipo excepción y activar el mecanismo que interrumpe el flujo normal del programa. Cuando el método `raiz` detecta un dato inválido, no devuelve un valor especial como en C, sino que ejecuta `throw new IllegalArgumentException(...)`. Esto indica explícitamente que la función no puede continuar y que el problema debe ser tratado en un nivel superior. En este momento, la ejecución del método termina de forma inmediata, sin continuar con las instrucciones restantes.

Controlar o capturar una excepción significa rodear el código que podría fallar con un bloque `try–catch`. Si el método llamado lanza una excepción, el flujo salta automáticamente hasta el `catch` correspondiente, donde se puede informar al usuario, registrar el error o tomar medidas de recuperación. Si el `main` llama a `Calculadora.raiz(-9)` dentro de un `try`, el `catch (IllegalArgumentException e)` recibe el objeto excepción y permite manejarlo desde fuera de la función que lo produjo. De esta forma, el error no provoca la detención brusca del programa y la aplicación puede continuar funcionando.

La propagación ocurre cuando un método no captura la excepción y, por tanto, esta se desplaza hacia arriba en la pila de llamadas. Cada método que aparece en esa cadena se interrumpe de inmediato y finaliza sin reanudarse en ningún momento. En el ejemplo, si `raiz` lanza la excepción y no existe ningún `catch` en métodos intermedios, la propagación continúa hasta llegar al `main`. Solo cuando aparece un bloque `catch` adecuado la propagación se detiene. Los métodos que quedaron “a medio ejecutar” no retoman su ejecución: simplemente se abandonan y se liberan de la pila.

Aplicado al ejemplo de la raíz cuadrada, si `raiz(-9)` lanza la excepción, la función termina en ese punto; si `main` contiene un `try–catch`, la excepción se controla allí, mostrando el mensaje al usuario. Si no hubiera `catch` en `main`, la excepción seguiría propagándose hasta el entorno de ejecución de Java, produciendo un error final. En ningún caso las funciones por las que pasa la excepción se reanudan, ya que la filosofía de las excepciones consiste precisamente en cortar de forma controlada la ejecución normal y delegar el manejo del problema en un punto específico del programa. Si quieres, puedo ilustrarlo con un esquema de la pila de llamadas paso a paso.

## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?

### Respuesta

La propagación natural de excepciones en Java ofrece varias ventajas importantes frente al enfoque tradicional de C basado en códigos de error. La primera ventaja es que permite **separar por completo la lógica del programa del manejo de errores**, ya que el código que detecta el fallo no tiene que decidir inmediatamente qué hacer con él. En lugar de devolver valores especiales y forzar al programador a comprobarlos tras cada llamada, la excepción viaja automáticamente por la pila hasta encontrar un punto adecuado donde gestionarse. Esto reduce código repetitivo y mejora considerablemente la legibilidad.

Otra ventaja es que la propagación garantiza que **la ejecución se detenga exactamente en el punto donde ocurre el error**, sin que continúen instrucciones que podrían dejar el programa en un estado inconsistente. En C, si un programador se olvida de comprobar un código de error, la función continúa ejecutándose y puede provocar fallos más graves. En cambio, en Java, la excepción corta la ejecución de forma automática y segura, evitando errores silenciosos difíciles de rastrear.

Además, la propagación permite un **manejo centralizado de errores**, ya que no es necesario capturar la excepción en cada nivel de la llamada. Un programa puede gestionar distintos tipos de errores desde un único bloque `catch` más arriba en la pila, reduciendo duplicación y facilitando modificaciones posteriores. En C esto resultaría muy complejo, porque habría que propagar manualmente códigos de error a través de todas las funciones intermedias, lo cual complica la arquitectura del programa.

Por último, las excepciones permiten transmitir **información detallada** sobre el fallo, como mensajes explicativos o incluso datos asociados al error. Los valores de retorno en C solo permiten transmitir números, y el programador debe diseñar estructuras adicionales si quiere más información. La excepción, en cambio, viaja como un objeto completo por la pila. Esto aporta potencia expresiva al lenguaje y hace que el diagnóstico de errores sea más claro y directo. Si quieres, puedo relacionar estas ventajas con el ejemplo concreto de la raíz cuadrada paso a paso.


## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?

### Respuesta

En orientación a objetos, las excepciones suelen representarse como **objetos**, y esta es una de las diferencias esenciales frente al manejo de errores tradicional en C. En Java, todas las excepciones derivan de clases de la jerarquía `Throwable`, lo que permite que una excepción transporte información completa sobre el error: un mensaje, el tipo concreto de problema y la traza de la pila. Al ser objetos, pueden encapsular datos y comportamientos que describen con precisión la causa del fallo, en lugar de limitarse a simples códigos numéricos como ocurre en C.

Desde el punto de vista de la **encapsulación**, este enfoque ofrece varias ventajas. La lógica que describe el error queda agrupada en un único objeto, lo que permite definir mensajes adecuados, comportamientos específicos y, si es necesario, información adicional. Esto facilita que el código cliente reciba una descripción clara del error sin necesidad de conocer detalles internos de cómo se detectó. Además, el tipo de la excepción permite distinguir de forma estructurada entre diferentes problemas sin depender de convenciones frágiles como "si devuelve -1 es error".

Gracias a que las excepciones son objetos, es perfectamente posible **crear excepciones personalizadas**. El programador puede definir sus propias clases de excepción extendiendo `Exception` o `RuntimeException`, lo que permite modelar errores propios del dominio del programa. Por ejemplo, en un sistema de cálculo podría definirse una excepción como `RaizNegativaException` para distinguir ese caso específico de otros fallos numéricos. Esta personalización mejora la claridad del código y facilita que distintos errores se manejen de manera diferenciada.

Esta capacidad de crear nuevas clases de excepción refuerza la filosofía de la programación orientada a objetos: cada tipo de problema puede representarse con su propia entidad autónoma, capaz de describirse y gestionarse adecuadamente. En conjunto, este modelo proporciona una forma más expresiva, organizada y mantenible de manejar errores que los enfoques tradicionales no orientados a objetos. Si quieres, puedo crear un ejemplo con una excepción personalizada para el caso de la raíz cuadrada.

## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?

### Respuesta

Un objeto excepción en Java siempre transporta **información esencial** que resulta muy útil al llegar a un manejador (`catch`). La primera pieza fundamental es un **mensaje descriptivo** (`String message`) que explica la causa del error. Este mensaje suele proporcionar contexto suficiente para comprender qué ha fallado sin necesidad de inspeccionar el código internamente. En el ejemplo de la raíz cuadrada, un mensaje como *"No se puede calcular la raíz de un número negativo"* permite identificar inmediatamente el problema, algo que en C habría que reconstruir manualmente a partir de valores especiales o códigos de error.

Además del mensaje, una excepción contiene la **traza de la pila de llamadas** (*stack trace*), que es un registro detallado de todos los métodos que estaban activos en el momento exacto del fallo. Esta información es crucial porque muestra en qué punto del programa se originó el problema y cómo se llegó hasta ese lugar. En C, reconstruir esta información requiere herramientas externas o depuración avanzada, mientras que en Java el propio objeto excepción ya la lleva encapsulada de forma automática.

La fusión de estos dos elementos —mensaje explicativo y traza completa de la pila— proporciona un diagnóstico inmediato y muy preciso cuando la excepción llega al manejador. Esto permite tanto informar correctamente al usuario como facilitar enormemente la depuración del programa, ya que el desarrollador puede localizar el origen del fallo sin recurrir a comprobaciones manuales ni a impresiones de depuración distribuidas por el código.

En conjunto, esta riqueza de información encapsulada en cada objeto excepción constituye una mejora significativa respecto al enfoque de C, donde el programador debe construir sus propios mecanismos de diagnóstico. Gracias a este diseño, Java ofrece un modelo de tratamiento de errores más claro, más seguro y mucho más expresivo. Si quieres, puedo mostrar cómo imprimir y analizar una traza de pila usando el ejemplo de la raíz cuadrada.


## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?

### Respuesta

Sí, en Java es posible colocar **más de un bloque `catch`** después de un mismo bloque `try`. Esta estructura permite capturar **distintos tipos de excepciones por separado**, lo que resulta útil cuando una misma zona de código puede producir errores de naturalezas diferentes. Cada bloque `catch` se asocia a un tipo concreto de excepción, y el lenguaje selecciona automáticamente el primero cuyo tipo sea compatible con la excepción lanzada.

Sin embargo, **solo se ejecuta un único bloque `catch`** por excepción. Cuando ocurre un error dentro del `try`, el mecanismo de excepciones busca desde arriba hacia abajo el primer `catch` que coincida con el tipo exacto o con una superclase del tipo lanzado. En cuanto encuentra uno adecuado, lo ejecuta y **no continúa evaluando los demás**. Este comportamiento evita ambigüedades y mantiene el flujo de control claro y determinista.

Este diseño también obliga a ordenar los bloques `catch` de forma correcta: primero los tipos más específicos y después los más generales. Si se pusiera arriba un tipo de excepción demasiado general, como `Exception`, bloquearía la posibilidad de que `catch` más específicos llegasen a ejecutarse, dando lugar a un error de compilación. Por ello, Java exige que la jerarquía se respete de manera estricta, garantizando un manejo estructurado del error.

La posibilidad de usar varios `catch` permite escribir código más preciso y modular. Un mismo fragmento en el `try` puede desencadenar errores diferentes, y cada uno puede requerir un tratamiento distinto. Gracias a esta característica, el programador puede proporcionar respuestas diferenciadas sin mezclar lógicas de error variadas dentro de un único bloque. Si quieres, puedo incluir un ejemplo concreto con varios `catch` aplicado al caso de la raíz cuadrada.

## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

### Respuesta

Para garantizar que cierto código **se ejecute siempre**, incluso cuando ocurre una excepción y antes de que esta continúe propagándose, Java proporciona el bloque **`finally`**. El bloque `finally` se ejecuta **siempre**, haya o no `catch`, haya o no excepción, incluso aunque dentro del `try` aparezcan `return` o instrucciones que terminarían normalmente el método. Esta característica permite asegurar el cierre de ficheros, liberación de recursos o cualquier acción crítica que deba realizarse sin condiciones.

El `finally` resulta especialmente útil porque las excepciones pueden interrumpir abruptamente el flujo normal del programa. Si un método lanza una excepción y no existe un `finally`, el código que debería liberar recursos podría no llegar a ejecutarse. Gracias al `finally`, se garantiza que la limpieza final de recursos se realiza antes de continuar con la propagación de la excepción o antes de volver al flujo normal si la excepción ha sido capturada por un `catch`.

A continuación se muestran los dos ejemplos solicitados: primero uno con `catch` y `finally`, y luego otro con `try` más `finally` sin `catch`. Ambos ilustran cómo asegurar que un recurso se cierra siempre, sin importar lo que ocurra dentro del `try`.

***

## ✔️ Ejemplo con `try–catch–finally`

En este caso, la excepción se captura y después se ejecuta siempre el `finally`.

```java
public class EjemploConCatch {

    public static void main(String[] args) {
        java.io.FileReader fr = null;

        try {
            fr = new java.io.FileReader("datos.txt");
            System.out.println("Leyendo archivo...");
            // Simulación de error
            double r = Calculadora.raiz(-9);
        } catch (Exception e) {
            System.out.println("Error capturado: " + e.getMessage());
        } finally {
            System.out.println("Cerrando recursos (finally)...");
            if (fr != null) {
                try {
                    fr.close();
                } catch (Exception e) {
                    System.out.println("Error cerrando fichero.");
                }
            }
        }

        System.out.println("El programa continúa.");
    }
}
```

Aquí, pase lo que pase en el `try`, el fichero se intenta cerrar en el `finally`.

***

## ✔️ Ejemplo con `try–finally` *sin* `catch`

Este patrón se usa cuando se desea que la excepción **se propague**, pero aun así asegurando la liberación de recursos.

```java
public class EjemploSinCatch {

    public static void main(String[] args) throws Exception {
        java.io.FileReader fr = null;

        try {
            fr = new java.io.FileReader("datos.txt");
            System.out.println("Leyendo archivo...");
            // Este error no se captura aquí
            double r = Calculadora.raiz(-9);
        } finally {
            System.out.println("Cerrando recursos (finally)...");
            if (fr != null) {
                try {
                    fr.close();
                } catch (Exception e) {
                    System.out.println("Error cerrando fichero.");
                }
            }
        }

        // Este mensaje no se ejecutará, porque la excepción se propagó
        System.out.println("Esto no se mostrará.");
    }
}
```

En este segundo ejemplo, el `finally` **se ejecuta**, pero después la excepción sigue su camino hacia arriba en la pila porque no se ha capturado.

## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

### Respuesta

Sí, en Java el bloque `finally` **puede aparecer sin ningún bloque `catch`**, siempre que vaya asociado a un `try`. Este patrón se utiliza cuando se desea que se ejecute un código obligatorio de limpieza, pero dejando que la excepción se siga propagando hacia fuera. En ese caso, el `finally` garantiza que la operación crítica (como cerrar un fichero o liberar un recurso) ocurra antes de que el error llegue al siguiente nivel de la pila de llamadas. Es un mecanismo útil cuando se quiere combinar seguridad en la limpieza con simplicidad en el manejo de errores.

El bloque `finally` **se ejecuta siempre**, tanto si ocurre una excepción como si no ocurre ninguna. Esto incluye llamadas normales, que no generan errores, y también situaciones en las que se lanza una excepción que luego se captura o se deja propagar. Esta ejecución incondicional permite asegurar que el programa no deje recursos abiertos o estados inconsistentes. Incluso si en el `try` aparece un `return`, el control pasa primero por el `finally` antes de salir definitivamente del método, lo que garantiza la limpieza sin importar la forma en la que termina el bloque `try`.

Sin embargo, existen algunos casos extremos en los que el `finally` no se ejecuta, como cuando el programa se detiene con `System.exit()`, cuando la JVM se cierra abruptamente o cuando ocurre un fallo irrecuperable a nivel del sistema (por ejemplo, un *crash* de la JVM). Fuera de estas situaciones excepcionales, Java asegura que el `finally` actúe como un punto de paso obligatorio antes de abandonar el `try`, con o sin `catch`, y ocurra o no una excepción.

Este comportamiento puede ilustrarse fácilmente con un pequeño ejemplo. En el siguiente fragmento, aunque el método devuelve un valor desde dentro del `try`, el código del `finally` se ejecuta siempre antes de abandonar el método:

```java
public static int ejemplo() {
    try {
        System.out.println("Dentro de try");
        return 42;   // incluso aquí, el finally se ejecuta
    } finally {
        System.out.println("Ejecutando finally");
    }
}
```

Al llamar a `ejemplo()`, la consola mostrará primero el mensaje del `try` y después el del `finally`, antes de devolver finalmente el valor retornado. Si deseas, puedo mostrar también una versión con una excepción para observar cómo se ejecuta `finally` antes de que la excepción se propague.

## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

### Respuesta

En Java, las excepciones se dividen en **controladas (checked)** y **no controladas (unchecked)**, y esta distinción determina si el compilador obliga o no a tratarlas. Las **excepciones controladas** son aquellas que el compilador exige capturar con un bloque `try–catch` o bien declarar con `throws`. Se usan para representar errores que el programador *debe prever* y que suelen depender de factores externos, como ficheros, red o dispositivos. En cambio, las **excepciones no controladas** son aquellas que derivan de `RuntimeException` y que **no requieren** ser declaradas ni capturadas. Representan errores de programación, como acceder fuera de un array o dividir entre cero, situaciones que normalmente indican un fallo lógico más que un caso recuperable.

La clase `RuntimeException` juega un papel central porque marca el punto de separación entre ambos tipos. Todas las excepciones que heredan de ella son **no controladas**, lo que indica que no se espera que el código las maneje explícitamente. Esto se debe a que suelen reflejar errores que deberían corregirse en el propio código y no mediante recuperación. Por el contrario, cualquier excepción que **no** derive de `RuntimeException` es controlada, y el compilador asegurará que el programador tome una decisión explícita sobre cómo tratarla. Este mecanismo fomenta una programación más robusta y evita que se ignoren situaciones críticas relacionadas con recursos externos.

A continuación se muestran ejemplos representativos. Entre las **excepciones controladas** típicas se encuentran `IOException` al trabajar con ficheros, `SQLException` al acceder a bases de datos y `FileNotFoundException` al intentar abrir un archivo inexistente. Estas situaciones dependen del entorno y deben gestionarse para que el programa pueda recuperarse o informar adecuadamente al usuario. Entre las **no controladas**, habituales se encuentran `NullPointerException`, `ArrayIndexOutOfBoundsException` y `ArithmeticException`, que indican errores de programación y suelen corregirse modificando el código. Aunque también se pueden crear excepciones personalizadas en ambos grupos, la elección depende de si se desea obligar al usuario de la clase a manejar el error o dejarlo como un fallo no recuperable.

Por último, se presentan dos listas con situaciones donde se prefiere cada tipo de excepción. Las **excepciones controladas** suelen preferirse cuando la operación depende del exterior: apertura de ficheros, comunicación por red, acceso a bases de datos o lectura de dispositivos. En cambio, las **no controladas** son apropiadas cuando se detectan errores internos del programa: parámetros inválidos pasados por un desarrollador, violaciones de precondiciones, errores de lógica o intentos de operar sobre estados ilegales de un objeto. Esta clasificación permite que el código comunique de forma clara la naturaleza del error y el nivel de responsabilidad del programador al tratarlo.

***

# ✔️ Ejemplos típicos

### **Excepciones controladas (checked)**

Son obligatorias de capturar o declarar.

*   `FileNotFoundException` — apertura de un archivo que puede no existir.
*   `IOException` — lectura o escritura que puede fallar por causas externas.
*   `SQLException` — errores al conectarse o consultar una base de datos.
*   `ClassNotFoundException` — carga dinámica de clases que podría no existir.

***

### **Excepciones no controladas (unchecked)**

Herederas de `RuntimeException`; no es obligatorio capturarlas.

*   `NullPointerException` — intentar usar un objeto que es `null`.
*   `ArithmeticException` — división entre cero.
*   `ArrayIndexOutOfBoundsException` — acceso fuera del rango de un array.
*   `IllegalArgumentException` — parámetro inválido pasado por el programador.

***

# ✔️ Situaciones donde se prefiere una **excepción controlada**

(Errores externos, previsibles y recuperables)

1.  Acceder a un archivo que puede faltar o estar protegido.
2.  Enviar datos por red, donde puede haber desconexiones.
3.  Consultar una base de datos que podría no estar disponible.
4.  Leer un dispositivo externo cuyo estado es incierto.

***

# ✔️ Situaciones donde se prefiere una **excepción no controlada**

(Errores internos del programa, normalmente derivados de malos parámetros)

1.  Recibir un parámetro negativo donde no tiene sentido (como la raíz cuadrada).
2.  Intentar acceder a un índice inválido en una estructura de datos.
3.  Pasar `null` cuando no está permitido.
4.  Romper precondiciones del objeto por un mal uso del API.

## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

### Respuesta

En Java, la palabra clave **`throws`** se utiliza para *declarar* que un método **puede lanzar** una excepción controlada durante su ejecución. Esta declaración no lanza la excepción por sí misma, sino que informa al compilador y a los métodos que llamen a este método de que deben estar preparados para tratar dicho error. De esta forma, se establece un contrato explícito: si el método falla por una causa prevista, no es él quien gestionará el problema, sino quien lo llame. Esto permite diseñar métodos más simples cuando la responsabilidad del manejo debe delegarse a niveles superiores del programa.

`throws` es una alternativa a capturar una excepción controlada porque el compilador obliga a elegir entre **dos opciones**: o bien se captura la excepción con un bloque `try–catch`, o bien se declara en la cabecera del método con `throws`. Si el programador considera que el método actual no es el lugar adecuado para gestionar ese tipo de error, entonces la opción más limpia consiste en delegarlo mediante `throws`. De esta forma, el método evita mezclarse con lógicas de error que no le pertenecen, y el tratamiento se realiza en un lugar más apropiado, como en un método de nivel superior, donde se disponga de más información para decidir qué hacer.

Este mecanismo es especialmente útil en situaciones donde el método es de bajo nivel y su única responsabilidad es realizar una operación concreta. Por ejemplo, si un método intenta abrir un fichero y este no existe, la excepción controlada `IOException` puede declararse con `throws`. Así, el método no se ve obligado a decidir cómo actuar ante la ausencia del fichero, dejando esa responsabilidad al llamador, que es quien realmente sabe cómo responder: mostrar un mensaje, pedir otro fichero o cancelar la operación. Con ello, se mantiene una estructura clara y coherente entre responsabilidades.

En conjunto, `throws` forma parte esencial del sistema de **excepciones controladas** en Java, ya que permite que la obligación impuesta por el compilador se cumpla sin necesidad de capturar la excepción inmediatamente. Gracias a este mecanismo, cada método decide si gestiona el error o si lo propaga, manteniendo una arquitectura flexible, escalable y fácil de mantener. Si lo deseas, puedo añadir un ejemplo completo comparando el uso de `try–catch` frente al uso de `throws` para un mismo método.

## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

### Respuesta

Cuando un método en Java declara `throws IOException`, está indicando que no desea tratar directamente los problemas relacionados con la apertura o manipulación del fichero. En este caso, si el fichero no existe, se lanzará una `FileNotFoundException` (subclase de `IOException`) que no se captura dentro del método, permitiendo que la excepción se propague al llamador. Este mecanismo evita mezclar en un mismo método tanto la lógica principal como el manejo de errores, manteniendo separadas sus responsabilidades.

A pesar de que el método no captura la excepción, sigue siendo necesario garantizar la liberación de los recursos abiertos, como el fichero. Para ello se emplea `finally`, que se ejecuta siempre, incluso si la excepción se produce dentro del `try`. De este modo se asegura que, aunque el fichero no pueda abrirse o surja cualquier problema durante la lectura, el recurso se intente cerrar antes de propagar la excepción hacia el exterior.

Este patrón resulta muy habitual cuando se implementan métodos de bajo nivel que simplemente realizan una operación concreta y no disponen del contexto adecuado para decidir qué hacer cuando algo falla. Al delegar el manejo de errores al método que llama, se permite que ese nivel superior tome decisiones informadas, como mostrar un mensaje al usuario, pedir un nuevo nombre de fichero o interrumpir la operación.

***

## ✔️ Ejemplo en Java con `throws` y con `finally`

```java
import java.io.FileReader;
import java.io.IOException;

public class LectorArchivos {

    // Método que NO maneja la excepción: la declara con throws
    public static void abrirYLeer(String nombreFichero) throws IOException {
        FileReader fr = null;

        try {
            fr = new FileReader(nombreFichero);
            System.out.println("Fichero abierto correctamente.");
            // Aquí podría leerse el contenido...
        } finally {
            System.out.println("Ejecutando finally para liberar recursos...");
            if (fr != null) {
                fr.close();   // puede lanzar IOException, se propaga también
            }
        }
    }

    public static void main(String[] args) {
        try {
            abrirYLeer("inexistente.txt");  // produce FileNotFoundException
        } catch (IOException e) {
            System.out.println("Error recibido desde arriba: " + e.getMessage());
        }
    }
}
```

## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

### Respuesta

Sí, técnicamente es posible poner excepciones **no controladas** (las que heredan de `RuntimeException`) en la cláusula `throws`. El lenguaje no lo prohíbe, ya que `throws` simplemente declara la posibilidad de que un método genere un determinado tipo de error. Sin embargo, esta práctica **no es necesaria** y casi nunca se utiliza, porque las excepciones no controladas no requieren ser declaradas ni capturadas. Su naturaleza implica que representan errores de programación, no situaciones externas recuperables.

El hecho de que un método declare `throws RuntimeException` **no obliga al método llamador a poner un bloque `try–catch`**, porque las reglas de compilación de Java solo exigen capturar o declarar las excepciones controladas. Si se decidiera añadir un `catch` para una excepción no controlada, no sería por obligación del compilador, sino por razones de diseño: un programador podría querer capturarla para registrar el error o detener el programa de forma más elegante. Aun así, en la mayoría de los casos no se recomienda capturarlas porque suelen indicar un fallo lógico que debe corregirse directamente en el código.

Añadir una excepción no controlada a `throws` solo tendría sentido en casos muy específicos, como cuando se desea documentar explícitamente que un método puede lanzar una excepción concreta de tipo `RuntimeException`, informando al desarrollador que usa el método sobre un posible uso incorrecto. Esto puede ayudar a clarificar la API, sobre todo en librerías. No obstante, esta documentación se considera opcional y no tiene impacto en el comportamiento del compilador. En general, la filosofía de Java es que las excepciones no controladas fluyan libremente para señalar errores que deben solucionarse en el desarrollo, no manejarse durante la ejecución.

## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

### Respuesta

Las **excepciones controladas** se recomiendan cuando el error proviene de **factores externos** al programa y, por tanto, es razonable esperar que el código cliente pueda **recuperarse** o actuar de una forma alternativa. Casos típicos son la lectura de ficheros, el acceso a la red o a una base de datos. En estas situaciones, el programador no puede evitar que algo falle, pero sí puede decidir qué hacer cuando ocurre. Por ello, excepciones como `IOException` obligan al llamador a tratar el problema, garantizando así que no se ignora un error relevante del entorno. Este enfoque favorece un diseño robusto cuando las circunstancias externas son imprevisibles pero manejables.

Por el contrario, las **excepciones no controladas** se utilizan cuando el error representa un **fallo lógico del propio programa**, generalmente debido a un uso incorrecto del API. En estos casos se prefieren excepciones como `IllegalArgumentException`, porque el error no es recuperable en tiempo de ejecución: lo correcto es **corregir el código**, no capturar la excepción. Este tipo de excepciones permite que los fallos se detecten rápidamente durante las pruebas, ya que no obligan al programador a envolver cada llamada en un `try–catch`, lo que mantendría un código innecesariamente verboso y menos claro.

No todos los lenguajes distinguen entre excepciones controladas y no controladas. De hecho, Java es uno de los pocos lenguajes de uso común que implementa esta separación de forma estricta. Muchos lenguajes modernos —como Python, C#, JavaScript o C++— solo utilizan excepciones equivalentes a las **no controladas**, es decir, todas derivan de un mismo sistema y ninguna obliga al programador a capturarlas. Esto simplifica el modelo de excepciones y evita problemas derivados del exceso de obligatoriedad, como la proliferación de bloques `try–catch` innecesarios.

En los lenguajes que solo ofrecen una opción, la modalidad predominante es siempre la equivalente a las **excepciones no controladas**. La razón es que proporcionan un mecanismo flexible y ligero: permiten manejar errores cuando se desea, y dejar que se propaguen cuando el error debe tratarse en capas superiores. Este modelo es más cercano a la filosofía general de muchos lenguajes de programación modernos, donde se favorece la simplicidad del flujo y se evita imponer estructuras obligatorias salvo cuando aportan un beneficio claro. Si quieres, puedo añadir una comparación breve entre Java y otro lenguaje que conozcas, como C++ o Python.


## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

### Respuesta

Lanzar excepciones dentro de un bloque `catch` es totalmente válido y tiene sentido cuando se necesita **convertir** una excepción en otra más adecuada al contexto, o cuando el código que captura el error actual no puede resolverlo, pero sí puede transformarlo antes de enviarlo hacia arriba. Este mecanismo se conoce como *wrapping* o *encapsulación de excepciones*, y se usa para proporcionar información más clara o más específica al nivel superior que recibirá el error.

También es posible **relanzar la misma excepción** que se ha capturado usando simplemente `throw;`. Esto tiene sentido cuando el bloque `catch` necesita realizar alguna acción parcial —como registrar el error, limpiar un estado interno o mostrar un mensaje temporal— pero no puede completar realmente el manejo. En ese caso, el código realiza esas operaciones y después deja que la excepción siga su camino natural a través de la pila de llamadas. Este patrón combina el control local con la propagación del error.

Relanzar excepciones suele ser útil en capas intermedias de un programa, como servicios o utilidades, que deben garantizar algún tipo de consistencia interna pero no tienen la responsabilidad final sobre cómo reaccionar ante un fallo. Al relanzar la excepción original, se conserva información valiosa como el mensaje y la traza de pila, lo que facilita el diagnóstico. Por otro lado, lanzar una excepción distinta puede servir para ocultar detalles internos y exponer únicamente errores significativos para el nivel superior.

***

## ✔️ Ejemplo 1: lanzar una excepción distinta dentro del `catch`

(*Wrapping de excepciones*)

```java
public void leerFichero(String nombre) {
    try {
        FileReader fr = new FileReader(nombre);
    } catch (IOException e) {
        // Se lanza una excepción más apropiada para el contexto
        throw new IllegalStateException("No se pudo cargar la configuración", e);
    }
}
```

Aquí se captura una `IOException`, pero se transforma en una excepción de tipo `IllegalStateException` más coherente con el nivel superior del programa (por ejemplo, un módulo de configuración).

***

## ✔️ Ejemplo 2: relanzar la misma excepción capturada

(*Re-throw simple*)

```java
public void procesarDatos() throws IOException {
    try {
        FileReader fr = new FileReader("datos.txt");
    } catch (IOException e) {
        System.out.println("Registrando el error y re-lanzándolo...");
        throw e;   // se relanza la MISMA excepción
    }
}
```

En este caso, el método registra el error, pero lo envía de nuevo hacia arriba para que lo gestione quien lo haya llamado.

## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

### Respuesta

Cuando se dice que una excepción es la **“causa”** de otra excepción, se está indicando que una excepción de nivel inferior provocó otra de nivel superior que se lanza en su lugar. Esta relación permite mostrar no solo el error final, sino también el **origen real del problema**, manteniendo así un rastro completo de lo sucedido. En Java, esta asociación se realiza indicando la excepción original como parámetro en el constructor de la nueva excepción, lo que se conoce como *encapsulación* o *wrapping* de excepciones.

Este mecanismo se usa cuando una capa baja del programa lanza una excepción demasiado técnica o con detalles internos que no se desean exponer directamente. La capa superior puede capturarla, transformarla en una excepción más apropiada al contexto del módulo, y declararla como excepción causada por la original. De este modo, se mantiene la información técnica para diagnósticos, pero se ofrece al código cliente un error más significativo desde el punto de vista lógico o de dominio.

Cuando una excepción que tiene causa se muestra por pantalla —por ejemplo, usando `printStackTrace()`—, Java incluye automáticamente la información de la causa justo debajo de la traza de la excepción principal. Esto aparece con la palabra clave **`Caused by:`**, seguida de la traza completa de la excepción original. Gracias a este mecanismo, un desarrollador puede ver con claridad no solo el error final, sino también la cadena de fallos que lo originó, lo que facilita enormemente la depuración.

***

## ✔️ Ejemplo en Java: encapsulando una excepción de bajo nivel en una de alto nivel

En este ejemplo, se captura una `IOException` de bajo nivel y se encapsula dentro de una excepción personalizada más significativa para el dominio del programa:

```java
// Excepción personalizada de alto nivel
class ConfiguracionException extends Exception {
    public ConfiguracionException(String mensaje, Throwable causa) {
        super(mensaje, causa);
    }
}

public class LectorConfiguracion {

    public static void cargarConfiguracion(String nombre) throws ConfiguracionException {
        try {
            java.io.FileReader fr = new java.io.FileReader(nombre);
            // ... lectura hipotética ...
        } catch (java.io.IOException e) {
            // Se encapsula la excepción original como causa
            throw new ConfiguracionException("No se pudo cargar la configuración del sistema", e);
        }
    }

    public static void main(String[] args) {
        try {
            cargarConfiguracion("config.txt");
        } catch (ConfiguracionException e) {
            e.printStackTrace();  // aquí se verá también la causa
        }
    }
}
```

***

## ✔️ ¿Qué se verá por pantalla?

Cuando `printStackTrace()` se ejecute, aparecerá algo parecido a esto:

    ConfiguracionException: No se pudo cargar la configuración del sistema
        at LectorConfiguracion.cargarConfiguracion(LectorConfiguracion.java:12)
        ...
    Caused by: java.io.FileNotFoundException: config.txt (No such file or directory)
        at java.io.FileReader.<init>(FileReader.java:...)
        ...

La sección **“Caused by:”** muestra explícitamente la excepción original, conservando información valiosa como el tipo, el mensaje y la traza completa.

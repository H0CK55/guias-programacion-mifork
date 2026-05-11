<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Polimorfismo". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación, Excepciones, Composición y Herencia.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# Tema 5. Polimorfismo

## 1. Brevemente, ¿qué es el **"polimorfismo"** y para qué sirve en programación orientada a objetos? ¿qué es la **"sobreescritura"** de métodos?

### Respuesta

El polimorfismo es una característica de la programación orientada a objetos que permite tratar objetos de distintas clases de forma uniforme a través de una referencia común, normalmente la de su superclase o una interfaz. Gracias a esto, el mismo mensaje (llamada a un método) puede producir comportamientos distintos dependiendo del tipo real del objeto que lo recibe. Su principal utilidad es permitir escribir código más genérico, flexible y extensible.
La sobreescritura de métodos consiste en definir en una subclase un método con la misma firma (nombre, parámetros y tipo de retorno compatible) que uno heredado de la superclase, sustituyendo su implementación. Es el mecanismo concreto que hace posible el polimorfismo en tiempo de ejecución, ya que el método que finalmente se ejecuta depende del tipo real del objeto y no del tipo de la referencia.

## 2. ¿En qué consiste la **"ligadura dinámica"** o **"enlace tardío"**? ¿qué relación tiene con el polimorfismo? ¿hay que indicarlos explícitamente al programar o depende esto del lenguaje? Compara C++ y Java. Indicalo después también para Python.

### Respuesta

La ligadura dinámica (o enlace tardío) es el proceso por el cual la decisión de qué implementación de un método se ejecuta se toma en tiempo de ejecución, en lugar de en tiempo de compilación. Está directamente relacionada con el polimorfismo, ya que permite que una llamada a un método sobre una referencia del supertipo ejecute el método de la subclase correspondiente al objeto real.
En C++, la ligadura dinámica no es el comportamiento por defecto: es necesario marcar los métodos como virtual para que se resuelvan dinámicamente. En cambio, en Java, todos los métodos de instancia no estáticos ni final son dinámicos por defecto, por lo que el programador no necesita indicarlo explícitamente. Esto hace que el uso del polimorfismo sea más natural y frecuente.
En Python, todo es dinámico por naturaleza. Todas las llamadas a métodos se resuelven en tiempo de ejecución sin que exista un mecanismo explícito equivalente a virtual. El polimorfismo se basa en el tipo real del objeto y en la presencia de los métodos, no en jerarquías estrictas.


## 3. Pon un ejemplo sencillo en Java, de un `Soldado`, con un método `saluda`, con dos subclases: `Zapador` y `Artillero`, donde `Zapador` sobreescribe el método `saludar`, sustituyendo por completo su comportamiento. Ilustra el funcionamiento del polimorfismo creando un array de `Soldados` de dos tipos y luego recorriéndolo empleando referencias de tipo `Soldado` y llamando a `saludar`.

### Respuesta

El polimorfismo se aprecia claramente cuando una subclase sobreescribe un método heredado y, aun así, este se invoca mediante una referencia del tipo de la superclase. En el siguiente ejemplo, Zapador redefine completamente el método saludar, mientras que Artillero hereda el comportamiento original.

public class Soldado {
    public void saludar() {
        System.out.println("Soldado saludando");
    }
}

public class Zapador extends Soldado {
    @Override
    public void saludar() {
        System.out.println("Zapador listo para poner minas");
    }
}

public class Artillero extends Soldado {
}
``

Soldado[] ejercito = {
    new Zapador(),
    new Artillero()
};

for (Soldado s : ejercito) {
    s.saludar();
}

Aunque el array y las referencias son de tipo Soldado, el método ejecutado en cada caso depende del tipo real del objeto, lo que demuestra el polimorfismo.


## 4. Si sobreescribo un método, ¿puedo invocar el método base para trabajar a partir de su resultado? Haz que zapador cambie ligeramente la forma de saludar, que salude de forma normal, tal cual hace el soldado base, pero que además añada un "ZAPADOR A SUS ORDENES" ¿qué palabra clave del lenguaje has usado para invocar al método de la clase base?

### Respuesta

Al sobreescribir un método, es posible reutilizar parcial o totalmente el comportamiento original de la superclase. Para ello se utiliza la palabra clave super, que permite invocar directamente el método de la clase base.
En el caso del Zapador, se puede mantener el saludo básico del soldado y añadir un mensaje adicional, en lugar de sustituirlo por completo. Esto permite extender el comportamiento sin duplicar código.

public class Zapador extends Soldado {
    @Override
    public void saludar() {
        super.saludar();
        System.out.println("ZAPADOR A SUS ÓRDENES");
    }
}
La palabra clave empleada para invocar al método de la clase base es super.

## 5. Al sobreescribir un método en Java, ¿qué restricciones existen sobre los tipos de los parámetros y el tipo de retorno? ¿Qué diferencia hay entre sobreescritura (*overriding*) y sobrecarga (*overloading*)? ¿Para qué sirve la anotación `@Override` y por qué es recomendable usarla siempre?

### Respuesta

En Java, al sobreescribir un método, los parámetros deben ser exactamente iguales y el tipo de retorno debe ser el mismo o un subtipo del original (retorno covariante). Además, no se puede reducir la visibilidad del método heredado, aunque sí ampliarla.
La sobreescritura (overriding) redefine un método heredado y participa en el polimorfismo. La sobrecarga (overloading) consiste en definir varios métodos con el mismo nombre pero distintos parámetros dentro de una misma clase, y se resuelve en tiempo de compilación.
La anotación @Override indica explícitamente que un método pretende sobrescribir uno heredado. Es recomendable usarla siempre porque el compilador detecta errores (como firmas incorrectas) y se mejora la legibilidad y mantenibilidad del código.

## 6. Entonces, cuando se estudia Java, ¿se emplea el polimorfismo desde el principio? Por ejemplo, sobreescribiendo `toString` o sobreescribiendo `equals`, ¿ya estoy usando polimorfismo?

### Respuesta

Desde los primeros pasos en Java ya se está usando polimorfismo, aunque no siempre se sea consciente de ello. Al sobreescribir métodos como toString() o equals() heredados de Object, se está adaptando el comportamiento de esos métodos al tipo concreto de objeto.
Cuando una referencia de tipo Object invoca toString(), el método que se ejecuta es el correspondiente a la clase real del objeto. Esto es polimorfismo puro, y demuestra que no es una característica avanzada, sino un concepto central del lenguaje que se utiliza desde el inicio.

## 7. ¿Qué es una **"clase abstracta"**? ¿Qué es un **"método abstracto"**? ¿Puedo crear instancias de una clase abstracta? Pongamos un ejemplo en Java: Redefinamos `Soldado`, hagamos que, además del método `saluda` que ya tenía, tenga un método `atacar`, que sea abstracto y que cada tipo de soldado haga su acción cuando se le pida atacar. ¿Donde debemos poner `abstract`?

### Respuesta

Una clase abstracta es una clase que no puede instanciarse directamente y que está pensada para ser heredada. Un método abstracto es un método sin implementación, que obliga a las subclases concretas a proporcionar su propio comportamiento.
No se pueden crear instancias de una clase abstracta. En el siguiente ejemplo, Soldado define un comportamiento común (saludar) y obliga a las subclases a implementar el método atacar.

public abstract class Soldado {
    public void saludar() {
        System.out.println("Soldado saluda");
    }

    public abstract void atacar();
}

public class Zapador extends Soldado {
    @Override
    public void atacar() {
        System.out.println("Colocando minas");
    }
}

La palabra clave abstract debe colocarse tanto en la clase como en los métodos abstractos.


## 8. ¿Qué efecto tiene la palabra clave `final` sobre métodos y clases en Java? ¿Cómo se relaciona con el polimorfismo? ¿Conoces algún ejemplo de clase `final` en la propia API estándar de Java?

### Respuesta

La palabra clave final aplicada a un método impide que este sea sobreescrito en las subclases. Aplicada a una clase, evita que se herede de ella. Esto limita el polimorfismo, ya que se prohíbe la redefinición de comportamiento.
En la API estándar de Java existen ejemplos claros, como la clase String, que es final. Esto garantiza su inmutabilidad y evita alteraciones del comportamiento que podrían comprometer la seguridad o consistencia del lenguaje.

## 9. En Java, qué son las **"interfaces"**? ¿Son como clases abstractas? ¿Una clase puede implementar más de una interfaz?

### Respuesta

Una interfaz en Java define un conjunto de métodos que una clase debe implementar, sin proporcionar implementación (salvo métodos default). Conceptualmente se parece a una clase abstracta, pero establece un contrato más estricto.
Una clase puede implementar múltiples interfaces, lo que permite simular herencia múltiple de comportamiento abstracto sin los problemas asociados a la herencia múltiple de clases.


## 10. Vamos a poner un ejemplo nuevo con polimorfismo. Queremos implementar una clase `Punto`, con un método `calcularDistanciaA`, que permite calcular la distancia a otro `Punto`. Sin embargo, como queremos trabajar con puntos 2D y 3D, haz que ese método sea abstracto y haya dos implementaciones de ese cálculo de distancia. Emplea `instanceof` y *downcasting* para verificar que se recibe un punto compatible y poder calcular correctamente la distancia siempre entre puntos del mismo subtipo. Aprovecha este diseño para crear ahora una clase `Linea`, que acepta `Punto`, sin saber de qué tipo es, y es capaz de dar su longitud independientemente de las dimensiones de sus puntos (las cuales desconoce).

### Respuesta

Se puede definir una clase abstracta Punto con un método abstracto calcularDistanciaA. Las subclases Punto2D y Punto3D implementan el cálculo adecuado, verificando el tipo con instanceof y usando downcasting.

public abstract class Punto {
    public abstract double calcularDistanciaA(Punto otro);
}

public class Punto2D extends Punto {
    double x, y;

    public double calcularDistanciaA(Punto otro) {
        if (otro instanceof Punto2D) {
            Punto2D p = (Punto2D) otro;
            return Math.hypot(x - p.x, y - p.y);
        }
        throw new IllegalArgumentException();
    }
}

Una clase Linea puede trabajar con referencias Punto sin conocer su dimensión concreta, delegando el cálculo de la distancia en el propio polimorfismo.


## 11. ¿Qué es la **"herencia de interfaces"** en Java? ¿Existe **"herencia múltiple de interfaces"**? Pon un ejemplo de una interfaz `Fichero` que tenga un método para leer su contenido en forma de `String` y luego dicha interfaz sea extendida por otra que sea `FicheroEscribible` que permita enviar contenido e incluso eliminar el fichero.

### Respuesta

La herencia de interfaces permite que una interfaz extienda a otra, heredando sus métodos y ampliando el contrato. En Java sí existe herencia múltiple de interfaces, ya que una interfaz puede extender varias interfaces.

public interface Fichero {
    String leer();
}

public interface FicheroEscribible extends Fichero {
    void escribir(String contenido);
    void borrar();
}

Este mecanismo permite definir jerarquías de capacidades sin compartir implementación, manteniendo un diseño flexible y desacoplado.
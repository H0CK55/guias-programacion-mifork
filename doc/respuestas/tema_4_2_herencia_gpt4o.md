<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Herencia". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación, Excepciones y Composición.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# Tema 4.2. Herencia

## 1. En orientación a objetos, ¿qué es la **herencia** y su relación con "A es-un B"?. Explica las dos implicaciones principales: (1) **compatibilidad de tipos** y (2) **herencia de estado y comportamiento**. Pon un ejemplo en Java muy sencillo, donde un `Soldado` tiene un `nombre` (privado) y un método `saludar()` que muestra su nombre. Hay dos subtipos: un `Artillero`, que es capaz de disparar cohetes y un `Zapador` que pone minas, ambos heredan el atributo nombre y la capacidad de saludar. Además, y de forma específica, el artillero tiene un número de cohetes y el zapador un número de minas, accesibles mediante "getters" específicos. Respecto a la compatibilidad de tipos, aprovechémosla: crea un array de `Soldado`, mete varios de distinto tipo (son todos compatibles con `Soldado`). Recórrela y que todos te saluden.

### Respuesta

En orientación a objetos, la herencia es un mecanismo que permite definir una clase nueva a partir de otra ya existente. La relación conceptual que expresa es “A es-un B”, lo que significa que un objeto del subtipo puede considerarse también como un objeto del supertipo. Si se afirma que un Artillero es un Soldado, entonces cualquier lugar donde se espere un Soldado puede aceptar un Artillero.
La herencia tiene dos implicaciones principales. La primera es la compatibilidad de tipos: una referencia del tipo de la superclase puede apuntar a objetos reales de cualquiera de sus subclases. La segunda es la herencia de estado y comportamiento: los atributos y métodos no privados de la superclase pasan a formar parte del subtipo, evitando duplicación de código y manteniendo coherencia funcional.

public class Soldado {
    private String nombre;

    public Soldado(String nombre) {
        this.nombre = nombre;
    }

    public void saludar() {
        System.out.println("Soy el soldado " + nombre);
    }
}

public class Artillero extends Soldado {
    private int cohetes;

    public Artillero(String nombre, int cohetes) {
        super(nombre);
        this.cohetes = cohetes;
    }

    public int getCohetes() {
        return cohetes;
    }
}

public class Zapador extends Soldado {
    private int minas;

    public Zapador(String nombre, int minas) {
        super(nombre);
        this.minas = minas;
    }

    public int getMinas() {
        return minas;
    }
}

-------------------------------------------------

Soldado[] ejercito = {
    new Artillero("Luis", 5),
    new Zapador("Ana", 3),
    new Artillero("Carlos", 2)
};

for (Soldado s : ejercito) {
    s.saludar();
}


## 2. Al crear los soldados concretos, ¿cuántos constructores se ejecutan y en qué orden? ¿Qué significa `super` dentro de un constructor? Si la clase base no tiene visible el constructor sin parámetros, ¿debo llamar a `super` siempre? 

### Respuesta

Al crear un objeto de una subclase, siempre se ejecutan dos constructores: primero el de la superclase y después el de la subclase. El orden es obligatorio y garantiza que la parte común del objeto (definida en la superclase) esté correctamente inicializada antes de añadir los atributos específicos del subtipo.
La palabra clave super dentro de un constructor se utiliza para invocar explícitamente un constructor de la superclase. Si la superclase no tiene un constructor sin parámetros visible, es obligatorio llamar de forma explícita a super(...). En caso contrario, el código no compilará, ya que Java no sabrá cómo inicializar la parte heredada.

## 3. Respecto a los objetos de subclases en memoria, los atributos privados de la superclase, ¿forman parte de una instancia de la subclase en memoria? En caso afirmativo ¿implica que se puedan usar desde el código de la subclase? Explícalo con el ejemplo de `Soldado` y alguna de sus subclases.

### Respuesta

Los atributos privados de la superclase sí forman parte de la instancia de una subclase en memoria. Un objeto Artillero contiene físicamente el atributo nombre definido en Soldado, aunque no sea visible directamente desde el código de la subclase.
Sin embargo, que el atributo exista en memoria no implica que se pueda acceder a él desde la subclase. El modificador private restringe el acceso exclusivamente a la propia clase. Por ello, un Artillero no puede usar nombre directamente, pero sí mediante métodos públicos o protegidos definidos en Soldado, como saludar()

## 4. ¿Qué implica en términos de **extensibilidad** de código el hecho de que sean compatibles a nivel de tipos? Ilustra esto añadiendo un nuevo tipo de `Soldado` y demostrando que el código para pedir el saludo a todos los soldados no se modifica.

### Respuesta

La compatibilidad de tipos permite escribir código abierto a la extensión pero cerrado a la modificación. Al programar contra la superclase (Soldado), el código no necesita conocer los subtipos concretos que existirán en el futuro.
Si se añade un nuevo tipo, por ejemplo Medico, que herede de Soldado, el código que recorre el array de soldados y llama a saludar() no necesita ningún cambio, ya que sigue trabajando con referencias del supertipo. Esto mejora la mantenibilidad y escalabilidad del sistema.

-----------------------------------------------------------

public class Medico extends Soldado {
    public Medico(String nombre) {
        super(nombre);
    }
}

## 5. En Java, cuando trabajo con referencias y herencia. ¿Puedo tener una referencia del supertipo que apunte a objetos reales de un subtipo? ¿Puedo invocar con la referencia del supertipo a métodos públicos del subtipo? ¿En qué consiste el **"upcasting"** y el **"downcasting"**? ¿Qué es el `instanceof`? Pon un ejemplo de recorrido de un array de `Soldado`, comprobando que, si el objeto real es un `Artillero`, solicite el número de cohetes que tiene y los imprima.

### Respuesta

En Java es perfectamente válido que una referencia del supertipo apunte a un objeto real de un subtipo. Esto es la base del polimorfismo. Sin embargo, usando dicha referencia solo se pueden invocar métodos definidos en el supertipo.
El upcasting es la conversión implícita de un subtipo a un supertipo, y es segura. El downcasting es la conversión inversa y requiere comprobación previa con instanceof, ya que puede provocar un error en tiempo de ejecución si el objeto no es del tipo esperado.

---------------------------------------------------------

for (Soldado s : ejercito) {
    if (s instanceof Artillero) {
        Artillero a = (Artillero) s;
        System.out.println("Cohetes: " + a.getCohetes());
    }
}


## 6. Respecto a la ocultación de información y herencia, ¿qué significa acceso **"protegido"** de métodos y/o atributos? ¿Cómo se implementa en Java? Pon un ejemplo de uso de en la clase `Soldado` para que su nombre sea protegido y pueda usarse en el método de poner bombas del `Zapador`.

### Respuesta

El acceso protegido permite que atributos o métodos sean accesibles desde la propia clase, desde las subclases y desde las clases del mismo paquete. Es un punto intermedio entre private y public.
En Java se implementa con la palabra clave protected. Esto es útil cuando se desea mantener encapsulación pero permitir que las subclases reutilicen parte del estado interno. Por ejemplo, el nombre del soldado puede ser protegido para que el Zapador lo use al poner minas.

----------------------------------------------------------

public class Soldado {
    protected String nombre;
    ...
}

public class Zapador extends Soldado {
    public void ponerMina() {
        System.out.println(nombre + " ha puesto una mina");
    }
}

## 7. En los lenguajes orientados a objetos ¿hay una **clase base** para todos los objetos? ¿Ocurre en todos los lenguajes? ¿Qué ocurre en Java?

### Respuesta

En muchos lenguajes orientados a objetos existe una clase base común para todos los objetos. No ocurre en todos los lenguajes, pero sí ocurre en Java.
En Java, todas las clases heredan directa o indirectamente de java.lang.Object. Esto permite que todos los objetos compartan métodos comunes como toString(), equals() o hashCode(), reforzando la uniformidad del lenguaje.

## 8. ¿Qué es la **"herencia múltiple"**? ¿Existe en Java herencia múltiple?

### Respuesta

La herencia múltiple permite que una clase herede de más de una superclase. Esto puede provocar ambigüedades, como el conocido “problema del diamante”, donde no queda claro qué implementación heredar.
Java no permite herencia múltiple de clases. En su lugar, permite implementar múltiples interfaces, lo que proporciona polimorfismo sin heredar implementación, evitando los problemas asociados a la herencia múltiple tradicional.

## 9. Las excepciones en los lenguajes orientados a objetos son objetos. Por tanto, se pueden crear excepciones personalizadas. Pon un ejemplo en Java de una excepción personalizada (`UsuarioNoEncontradoException`), que sea *no controlada* y que además este compuesto con un `Usuario`, para saber qué `Usuario` dio el problema. Permite además que se pueda incluir la causa, es decir, sobrecarga el constructor para tener una versión que permita añadir la causa subyacente. 

### Respuesta

En Java, las excepciones son objetos y pueden heredarse. Una excepción no controlada debe extender RuntimeException. Además, puede componerse con otros objetos, como un Usuario, para aportar más contexto al error.

--------------------------------------------------------------

public class UsuarioNoEncontradoException extends RuntimeException {
    private Usuario usuario;

    public UsuarioNoEncontradoException(Usuario usuario) {
        this.usuario = usuario;
    }

    public UsuarioNoEncontradoException(Usuario usuario, Throwable causa) {
        super(causa);
        this.usuario = usuario;
    }

    public Usuario getUsuario() {
        return usuario;
    }
}

## 10. Herencia vs. Composición. Se dice que no se debe emplear herencia simplemente por reutilizar código, es decir, que si quiero reutilizar código simplemente, no debo pensar en herencia como primera opción ¿por qué?

### Respuesta

La herencia no debe utilizarse únicamente para reutilizar código, porque introduce una relación fuerte y permanente entre clases. Si la relación “es-un” no es conceptualmente correcta, el diseño se vuelve frágil y difícil de mantener.
Reutilizar código sin una relación semántica adecuada puede generar jerarquías artificiales y dependencias innecesarias, lo que dificulta la evolución futura del sistema.


## 11. Herencia vs. Composición. Se dice que se debe *"favorecer la composición frente a la herencia"*, ¿por qué?

### Respuesta

La composición permite construir clases a partir de otras mediante delegación, en lugar de heredar su comportamiento. Esto proporciona mayor flexibilidad, ya que los componentes pueden cambiarse sin afectar a la jerarquía de tipos.
Además, la composición reduce el acoplamiento y evita que los cambios en una superclase tengan efectos inesperados en todas sus subclases.


## 12. Herencia vs. Composición. Se dice que la *"herencia rompe la encapsulación"*, ¿a qué se refiere esto?

### Respuesta

Se dice que la herencia rompe la encapsulación porque las subclases pueden depender de detalles internos de la superclase. Si estos detalles cambian, el comportamiento de las subclases puede verse afectado.
Esto supone que la superclase no puede modificarse libremente sin considerar a todas sus subclases, lo que incrementa el acoplamiento y complica el mantenimiento.


## 13. Pongamos un ejemplo de dos alternativas para lo mismo. Tenemos un `Estudiante` y un `Trabajador`, ambos tienen datos en común: el DNI y el nombre. Modelemos esto de dos formas: uno por herencia, con una superclase `Persona`, y otro con composición, con una clase `DatosPersonales`. Se debe recibir una instancia de `DatosPersonales` en el constructor de la clase `Estudiante` y `Trabajador`.

### Respuesta

Opción 1: Herencia
public class Persona {
    protected String dni;
    protected String nombre;
}

public class Estudiante extends Persona { }
public class Trabajador extends Persona { }

Opción 2: Composición
public class DatosPersonales {
    private String dni;
    private String nombre;

    public DatosPersonales(String dni, String nombre) {
        this.dni = dni;
        this.nombre = nombre;
    }
}

public class Estudiante {
    private DatosPersonales datos;

    public Estudiante(DatosPersonales datos) {
        this.datos = datos;
    }
}

public class Trabajador {
    private DatosPersonales datos;

    public Trabajador(DatosPersonales datos) {
        this.datos = datos;
    }
}
En el segundo caso no se fuerza una relación “es-un”, se reduce el acoplamiento y se gana flexibilidad de diseño.
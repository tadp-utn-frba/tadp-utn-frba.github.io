---
layout: page
description: Instalación de Scala-IDE y otras guías
---

# Entorno de Trabajo

Para trabajar en Scala se debe instalar [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/index.html) (*Scala-IDE for Eclipse* requiere JDK 6, 7 ó 8).

Además, aunque se puede desarrollar sin un IDE (sólo se necesita un compilador), vamos a explicar como preparar un entorno de desarrollo. Se puede realizar de cualquiera de las siguientes 2 maneras:

1. Bajar e instalar [Scala IDE for Eclipse SDK](http://scala-ide.org/download/sdk.html)[^1]. *Scala IDE for Eclipse* es Eclipse con los plugins de Scala ya instalados.
2. Bajar Eclipse e instalar el plugin:
    * Bajar el [Eclipse](http://www.eclipse.org/downloads/)[^1] que más te guste. Recomendamos Eclipse IDE for Java EE Developers.
    * Instalarle el plugin del [Scala IDE for Eclipse](http://scala-ide.org/download/current.html). Asegurarse que coincida la versión del plugin con la versión de Eclipse que hayas instalado. Para hacer esto, hacer click en *Help > Install New Software…* Luego hacer click en el boton *Add*; y en la nueva ventana escribir un nombre para identificarlo, y pegar el link que aparece en el sitio que se hizo referencia al principio de este punto. Hacer click en *Ok*. Seleccionar **todos** los ítems de *Scala IDE for Eclipse* y también *Scala Worksheet*, que se encuentra en *Scala IDE plugins (incubation)*. Poner siguiente, y luego aceptar los términos y condiciones (que siempre se leen ¬¬)

## Versiones

Al día 17 de Agosto del 2015, las versiones de los entornos de trabajo son:

1. Scala IDE for Eclipse SDK 4.1.1:
    * Eclipse 4.4.2 (Luna)
    * Scala IDE 4.1.1
    * Scala 2.11.7
    * Scala Worksheet 0.3.0
2. Eclipse IDE for Java EE Developers:
    * Eclipse 4.5.0 (Mars)
    * Scala IDE 4.1.1
    * Scala 2.11.7
    * Scala Worksheet 0.3.0

# Creación de proyectos con tests

Para crear un proyecto ir al menú *File > New > Scala Project*. Si no aparece la opción, seleccionar *Other...* y buscar ahí la opción *Scala Project*.

En la primer pantalla de *New Scala Project* ingresar el nombre del proyecto, seleccionar el JRE a utilizar y luego seleccionar *Next >*.

En la segunda pantalla se puede agregar las carpetas para acomodar el proyecto (para separar carpetas de src y test); en la pestaña Libraries, hacer click en el botón *Add Library…* y ahí seleccionar **JUnit**, clickear el botón *Next >* y en esta nueva pantalla, en *JUnit library version*, seleccionar **JUnit 4** y hacer click en *Finish*. De nuevo en la pantalla de *New Scala Project* hacer click en *Finish* para finalizar la creación del proyecto.

Con el proyecto creado, crear un *Package* en las carpetas *src* y *test* (utilizar el mismo nombre del package en ambos). En el paquete ubicado en src crear una *Scala Class* con la clase de dominio. Y en el paquete ubicado en test crear otra *Scala Class* para la creación de los tests.

Para los tests tener en cuenta los siguientes imports:

* import org.junit.Before: Para poder utilizar el tag @Before y definir código que se debe ejecutar previo a cada test.
* import org.junit.Test: Para utilizar el tag @Test para indicar los tests, y que JUnit los reconozca y pueda correrlos.
* import org.junit.Assert._: Para utilizar métodos como assertEquals, assertTrue, etc. Que se utilizan para determinar si el test fue exitoso o no.

# Ejemplo de proyecto con tests

#### src.domain.Persona
{% highlight scala %}
package domain

class Persona (var edad) {
  def cumpliAnio = {
    edad += 1
  }
}
{% endhighlight %}

#### test.domain.Persona_Test
{% highlight scala %}
package domain

import org.junit.Before
import org.junit.Test
import org.junit.Assert._

class Persona_Test {
  var persona:Persona = null

  @Before
  def setup() = {
     persona = new Persona(1)
  }

  @Test
  def cumpliAnio_test() = {
    persona.cumpliAnio()
    assertEquals(2, persona.edad)
  }
}{% endhighlight %}

# Correr Tests

Para correr los tests, hacer click derecho en el paquete, archivo .scala o test particular, ir a la opción *Run As* y luego hacer click en *Scala JUnit Test*.

#### Notas al pie

[^1]: Fijate de elegir uno que se adapte al sistema operativo de tu PC y que sea de 32 o 64 bits según corresponda (esta es la única herramienta dependiente de la plataforma, las demás deberían servir tanto para diferentes sistemas operativos como para diferentes arquitecturas de procesador).

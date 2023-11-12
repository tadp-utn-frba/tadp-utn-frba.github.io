---
layout: page
description: Instalación de IDE y otras guías
---
# Intellij
## Instalación

1. Asegurate de tener instalada la JDK de Java 17 (o superior)
   - En la línea de comandos corré `javac -version` y asegurate de ver `javac 17.x.x` (o superior).
   - Si no tenés la versión 17 o superior, instalá la [JDK](https://docs.aws.amazon.com/corretto/latest/corretto-17-ug/downloads-list.html).
2. Luego, descargá e instalá [Intellij community edition](https://www.jetbrains.com/idea/download/)
3. Luego de iniciar Intellij, podés descargar e instalar el plugin de Scala:
   - File -> Settings -> Plugins -> buscar scala -> Install
   
      ![Plugins](/img/intellij_scala_plugin.png)
4. Reiniciar el IDE para que se apliquen los cambios

Más detalles y opciones en la página de [scala](https://docs.scala-lang.org/getting-started/intellij-track/getting-started-with-scala-in-intellij.html).

## Importar el proyecto sbt
1. Clonar el proyecto de github correspondiente a tu grupo
2. En intellij: File -> Open -> doble click en `build.sbt`

    ![Open project](/img/open_project.png)
3. Click en `Open as Project`
   
    ![Open as project](/img/open_as_project.png)

Para crear un proyecto desde cero, referirse a la página de scala ([con sbt](https://docs.scala-lang.org/getting-started/intellij-track/building-a-scala-project-with-intellij-and-sbt.html) y [sin sbt](https://docs.scala-lang.org/getting-started/intellij-track/getting-started-with-scala-in-intellij.html)).

## Escribiendo código scala
1. En el panel `Project` ubicado a la izquierda, expandí `{tu proyecto}` -> `src` -> `main` -> `scala` -> click derecho -> `New` -> `Package`
2. Nombrar el package `domain`
3. Click derecho sobre `domain` -> `New` -> `Scala class` -> nombrarla `Persona`

    ![Open as project](/img/create_person_class.png)
4. Cambiar el código a lo siguiente:

```scala
package domain

class Persona (var edad: Int) {
  def cumpliAnio = {
    edad += 1
  }
}
```

### Tests con ScalaTest
1. Agregar (o verificar que exista) la dependencia de ScalaTest en `build.sbt`
    ```scala
    libraryDependencies ++= Seq(
      "org.scalatest" %% "scalatest" % "3.2.9" % "test"
    )
    ```
2. Si recibís la notificación "build.sbt was changed", seleccionar `auto-import`.
3. Estas dos acciones van a producir que sbt descargue la biblioteca ScalaTest.
4. Esperá que la sincronización de sbt termine; de otra manera, intellij no va a reconocer el código de ScalaTest y el proyecto no va a compilar.
5. En el panel `Project` ubicado a la izquierda, expandí `{tu proyecto}` -> `src` -> `test` -> `scala` -> click derecho -> `New` -> `Package`
6. Nombrar el package `domain`
7. Click derecho sobre `domain` -> `New` -> `Scala class` -> nombrarla `PersonaTest`
8. Reemplazar el código por
    ```scala
    package domain
    
    import org.scalatest.freespec.AnyFreeSpec
    
    class PersonaTest extends AnyFreeSpec {
      "cuando una persona cumple años la edad debería ser 2" in {
        val persona = new Persona(1)
        persona.cumpliAnio
        assert(persona.edad == 2)
      }
    }
    ```
9. En el código, click derecho en `PersonaTest` y seleccionar `Run 'PersonaTest'`. Podés verificar el resultado de los test en el panel de abajo:

     ![Open as project](/img/scala_test_results.png)

Más detalles [acá](https://docs.scala-lang.org/getting-started/intellij-track/testing-scala-in-intellij-with-scalatest.html).

---
layout: page
description: Script Clase 8 TADP 1C2016
---

# Type Arguments y Varianza

## Introducción
Arrancamos con un repaso básico de tipos.

![](/scripts/granja.png)

~~~scala
var animal: Animal = ???
var vaca: Vaca = ???

animal.come
vaca.ordeñate
~~~

Tengo eso. Con que se puede inicializar?

~~~scala
var animal: Animal = new Vaca // Ok! Una vaca es un animal
var vaca: Vaca = new Animal   // No! Un animal no es necesariamente una vaca

animal.come
vaca.ordeñate
~~~

## Type Arguments

Hasta acá el tipado cierra. Llevemoslo un paso más mostrando colecciones. Armemos un conjunto de animales y tratemos de filtrar los que están gordos.

~~~scala
var miColeccion: Set = Set(new Vaca, new Caballo, new Granero)

miColeccion.filter{unElemento =>
  unElemento.estaGordo // Cómo sé si los elementos entienden esto?
}
~~~

Vemos que en este ejemplo no alcanza con decir que algo es una colección: Me va a importar también el tipo de las cosas que contiene.

De hecho, si recordamos el tipo de filter en Haskell era:

~~~haskell
filter::[a]->(a->Bool)->[a]
~~~

Es la misma operación la que me pide saber que tipo de elementos tiene. De acá se deduce que cualquier tipo podría requerir de un “subtipado”, dependiendo de los mensajes que queremos que entienda.

Scala me deja definir tipos que llevan parámetros (otros tipos) para poder contemplar estos escenarios.

Agregando esto, mi código quedaría:

~~~scala
var animales: Set[Animal] = Set(new Vaca, new Oveja, new Granero) // no me deja pasar granero porque no es un animal

animales.filter{ unElemento =>
    unElemento.estaGordo
}
~~~

El típo del mensaje filter va a ser muy parecido al de Haskell:

~~~haskell
#Set[A] >> filter(criterio: A=>Bool):Set[A]
~~~


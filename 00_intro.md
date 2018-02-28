{{meta {load_files: ["code/intro.js"]}}}

# Introducción

Este es un libro acerca de instruir ((computadora))s. Las computadoras son tan
comunes como los destornilladores hoy en dia. Pero son bastante más complejas
que los destornilladores, y hacer que hagan la cosa precisa que tu quieres
que hagan no siempre es fácil.

Si la tarea que tienes para tu computadora es común, y bien entendida,
como mostrar tu correo electrónico o funcionar como una calculadora,
puedes abrir la ((aplicación)) apropiada y ponerte a trabajar. Pero para
tareas únicas o abiertas, es posible que no haya una aplicación.

Ahí es donde la _((programación))_ podria entrar. La programación es el acto de
construir un programa: un conjunto de instrucciones precisas, que le dicen a una
computadora qué hacer. Porque las computadoras son bestias tontas y pedantes,
la programación es fundamentalmente tediosa y frustrante.

{{index [programming, "joy of"], speed}}

Afortunadamente, si puedes superar eso, y tal vez incluso disfrutar el rigor
de pensar en términos que las máquinas tontas puedan manejar, la programación
puede ser muy gratificante. Te permite hacer en segundos cosas que
tardarian _para siempre_ a mano. Es una forma de hacer que tu herramienta
computadora haga cosas que antes no podía hacer. Y proporciona un maravilloso
ejercicio en pensamiento abstracto.

La mayoría de la programación se realiza con ((lenguajes de programación)).
Un lenguaje de programación es un lenguaje construido artificialmente
utilizado para instruir ordenadores. Es interesante que la forma más efectiva
que hemos encontrado para comunicarnos con una computadora es bastante
parecida a la forma que usamos para comunicarnos entre nosotros.
Al igual que los idiomas humanos, los lenguajes de computación permiten
que las palabras y frases se combinen de nuevas maneras,
permitiendote expresar siempre nuevos conceptos.

{{index [JavaScript, "availability of"], "casual computing"}}

Las interfaces basadas en lenguajes, que en un momento fueron la principal
forma de interactuar con las computadoras para la mayoria de las personas,
han sido en gran parte reemplazadas con interfaces más simples y limitadas.
Pero todavía están allí, si sabes dónde mirar. Uno de esos idiomas,
JavaScript, está integrado en cada ((navegador)) web moderno y,
por lo tanto, está disponible en casi todos los dispositivos.

{{indexsee "web browser", browser}}

Este libro intentará familiarizarte lo suficiente con este lenguaje para
hacer cosas útiles y divertidas con él.

## Acerca de la programación

{{index [programming, "difficulty of"]}}

Además de explicar JavaScript, también introduciré los principios básicos
de la programación. La programación, resulta, es difícil. Las
reglas fundamentales son típicamente simples y claras. Pero los programas
construidos en base a estas reglas tienden a ser lo suficientemente
complejas como para introducir sus propias reglas y complejidad.
Estás construyendo tu propio laberinto, de alguna manera, y
es posible que te pierdas en él.

{{index learning}}

Habrá momentos en los que leer este libro se sentira terriblemente frustrante.
Si eres nuevo en la programación, habrá mucho material nuevo para
digerir. Gran parte de este material sera entonces _combinado_ en formas que
requerirán que hagas conexiones adicionales.

Depende de ti hacer el esfuerzo necesario. Cuando estes luchando
para seguir el libro, no saltes a ninguna conclusión acerca de tus propias
capacidades. Estás bien — solo tienes que seguir intentando.
Toma un descanso, vuelva a leer algún material, y _siempre_ asegúrate de
leer y comprender los programas de ejemplo y ((ejercicios)). Aprender es un
trabajo duro, pero todo lo que aprendes se convertira en tuyo y
el aprendimiento subsiguiente sera más fácil.

{{quote {author: "Ursula K. Le Guin", title: "La Mano Izquierda De La Oscuridad"}

{{index "Le Guin, Ursula K."}}

Cuando la acción deja de servirte, reune información; cuando la información
deja de servirte, duerme.

quote}}

{{index [program, "nature of"], data}}

Un programa es muchas cosas. Es una pieza de texto escrita por un programador,
es la fuerza directriz que hace que la computadora haga lo que hace,
es datos en la memoria de la computadora, y sin embargo controla las acciones
realizadas en esta misma memoria. Analogías que intentan comparar programas
a objetos con los que estamos familiarizados tienden a fallar. Una analogía
que es superficialmente adecuada es el de una máquina: muchas partes
separadas tienden a estar involucradas, y para hacer que funcione todo,
tenemos que considerar la formas en las que estas partes se interconectan y
contribuyen a la operación de un todo.

Una ((computadora)) es una máquina construida para actuar como anfitrión para
estas máquinas inmateriales. Las computadoras en si mismas solo pueden hacer
cosas estúpidamente sencillas. La razón por la que son tan útiles es que hacen
estas cosas a una ((velocidad)) increíblemente alta. Un programa puede
combinar ingeniosamente una enorme cantidad de estas acciones simples
para realizar cosas bastante complicadas.

{{index [programming, "joy of"]}}

Un programa es un edificio de pensamiento. No cuesta construirlo, no pesa
nada, y crece fácilmente bajo nuestras manos que teclean.

Pero sin ningun cuidado, el tamaño de un programa y su ((complejidad))
crecerán sin control, confundiendo incluso a la persona que lo creó.
Mantener programas bajo control es el problema principal de la programación.
Cuando un programa funciona, es hermoso. El arte de la programación es la
habilidad de controlar la complejidad. Un gran programa es moderado — hecho
simple en su complejidad.

{{index "programming style", "best practices"}}

Algunos programadores creen que esta complejidad se maneja mejor mediante
el uso de solo un pequeño conjunto de técnicas bien entendidas en sus
programas. Ellos han compuesto reglas estrictas ("mejores prácticas") que
prescriben la forma que los programas deberían tener, y se mantienen
cuidadosamente dentro de su pequeña y segura zona.

{{index experiment}}

Esto no solo es aburrido, sino que también es ineficaz. Nuevos problemas
a menudo requieren nuevas soluciones. El campo de la programación es joven y
todavía se esta desarrollando rápidamente, y es lo suficientemente variado
como para tener espacio para aproximaciones salvajemente diferentes.
Hay muchos errores terribles que hacer en el diseño de programas, así que
ve adelante y comételos para que los entiendas mejor. La idea de cómo se ve
un buen programa se desarrolla al practicar, no se aprende de una lista
de reglas.

## Por qué el lenguaje importa

{{index "programming language", "machine code", "binary data"}}

Al principio, en el nacimiento de la informática, no habían lenguajes
de programación. Los programas se veían mas o menos así:

```{lang: null}
00110001 00000000 00000000
00110001 00000001 00000001
00110011 00000001 00000010
01010001 00001011 00000010
00100010 00000010 00001000
01000011 00000001 00000000
01000001 00000001 00000001
00010000 00000010 00000000
01100010 00000000 00000000
```

{{index [programming, "history of"], "punch card", complexity}}

Ese es un programa que suma los números del 1 al 10 entre ellos e imprime
el resultado: `1 + 2 + ... + 10 = 55`. Podría ser ejecutado en una simple
máquina hipotética. Para programar las primeras computadoras, era necesario
colocar grandes arreglos de interruptores en la posición correcta o
perforar agujeros en tarjetas de cartón y darselos a la computadora.
Probablemente puedas imaginarte lo tedioso y propenso a errores que era este
procedimiento. Incluso escribir programas simples requería de mucha inteligencia
y disciplina. Los complejos eran casi inconcebibles.

{{index bit, "wizard (mighty)"}}

Por supuesto, ingresar manualmente estos patrones arcanos de bits (los unos
y ceros) le dieron al programador un profundo sentido de ser un poderoso
mago. Y eso tiene que valer algo en términos de satisfacción laboral.

{{index memory, instruction}}

Cada línea del programa anterior contiene una sola instrucción. Podría
ser escrito en español así:


```{lang: "text/plain"}
1. Almacenar el número 0 en la ubicación de memoria 0.
2. Almacenar el número 1 en la ubicación de memoria 1.
3. Almacenar el valor de la ubicación de memoria 1 en la ubicación de memoria 2.
4. Restar el número 11 del valor en la ubicación de memoria 2.
5. Si el valor en la ubicación de memoria 2 es el número 0,
   continuar con la instrucción 9.
6. Sumar el valor de la ubicación de memoria 1 a la ubicación de memoria 0.
7. Sumar el número 1 al valor de la ubicación de memoria 1.
8. Continuar con la instrucción 3.
9. Imprimir el valor de la ubicación de memoria 0.
```

{{index readability, naming, variable}}

Aunque eso ya es más legible que la sopa de bits, es aún dificil de entender.
Usar nombres en lugar de números para las
instrucciones y ubicaciones de memoria ayuda.

```{lang: "text/plain"}
 Establecer "total" como 0.
 Establecer "cuenta" como 1.
[loop]
 Establecer "comparar" como "cuenta".
 Restar 11 de "comparar".
 Si "comparar" es cero, continuar en [fin].
 Agregar "cuenta" a "total".
 Agregar 1 a "cuenta".
 Continuar en [loop].
[fin]
 Imprimir "total".
```

{{index loop, jump, "summing example"}}

¿Puedes ver cómo funciona el programa en este punto? Las primeras dos líneas
le dan a dos ubicaciones de memoria sus valores iniciales: se usará `total`
para construir el resultado de la computación, y `cuenta` hará un seguimiento
del número que estamos mirando actualmente. Las líneas usando
`comparar` son probablemente las más extrañas. El programa quiere ver
si `cuenta` es igual a 11 para decidir si puede detener su ejecución.
Debido a que nuestra máquina hipotética es bastante primitiva, esta solo puede
probar si un número es cero y hace una decisión (o salta) basándose en eso.
Por lo tanto, usa la ubicación de memoria etiquetada como
`comparar` para calcular el valor de `cuenta - 11` y toma una decisión
basada en ese valor. Las siguientes dos líneas agregan el valor de `cuenta`
al resultado e incrementan `cuenta` en 1 cada vez que el programa haya decidido
que `cuenta` todavía no es 11.

Aquí está el mismo programa en JavaScript:

```
let total = 0, cuenta = 1;
while (cuenta <= 10) {
  total += cuenta;
  cuenta += 1;
}
console.log(total);
// → 55
```

{{index "while loop", loop}}

Esta versión nos da algunas mejoras más. Lo más importante, ya
no es necesario especificar la forma en que queremos que el programa salte
hacia adelante y hacia atrás. El constructo del lenguaje `while` se ocupa
de eso. Este continúa ejecutando el bloque de código (envuelto en llaves)
debajo de el, siempre y cuando la condición que se le dio se mantenga.
Esa condición es `cuenta <= 10`, lo que significa "_cuenta_ es menor o igual a
10". Ya no tenemos que crear un valor temporal y compararlo con cero,
lo cual era un detalle sin interés. Parte del poder de los lenguajes de
programación es que se encargan de los detalles sin interés por nosotros.

{{index "console.log"}}

Al final del programa, después de que el constructo `while` haya terminado,
la operación `console.log` se usa para mostrar el resultado.

{{index "sum function", "range function", abstraction, function}}

Finalmente, aquí está cómo se vería el programa si tuvieramos acceso a las
las convenientes operaciones `rango` y `suma` disponibles, que
respectivamente crea una ((colección)) de números dentro de un rango y
calcula la suma de una colección de números:

```{startCode: true}
console.log(suma(rango(1, 10)));
// → 55
```

{{index readability}}

La moraleja de esta historia es que el mismo programa se puede expresar en
formas largas y cortas, ilegibles y legibles. La primera versión del
programa era extremadamente oscura, mientras que esta última es casi
Español: muestra en el `log` de la consola la `suma` del `rango` de los números
1 al 10. (En [capítulos posteriores](data) veremos cómo definir operaciones
como `suma` y `rango`)

{{index ["programming language", "power of"], composability}}

Un buen lenguaje de programación ayuda al programador permitiéndole
hablar sobre las acciones que la computadora tiene que realizar en un nivel
superior. Ayuda a omitir detalles poco interesantes, proporciona bloques
de construcción convenientes (como `while` y `console.log`), te permite
que definas tus propios bloques de construcción (como `suma` y `rango`),
y hace que esos bloques sean fáciles de componer.

## What is JavaScript?

{{index history, Netscape, browser, "web application", JavaScript, [JavaScript, "history of"], "World Wide Web"}}

{{indexsee WWW, "World Wide Web"}}

{{indexsee Web, "World Wide Web"}}

JavaScript was introduced in 1995 as a way to add programs to web
pages in the Netscape Navigator browser. The language has since been
adopted by all other major graphical web browsers. It has made modern
web applications possible—applications with which you can interact
directly, without doing a page reload for every action. But it is also
used in more traditional websites to provide various forms of
interactivity and cleverness.

{{index Java, naming}}

It is important to note that JavaScript has almost nothing to do with
the programming language named Java. The similar name was inspired by
marketing considerations, rather than good judgment. When JavaScript
was being introduced, the Java language was being heavily marketed and
was gaining popularity. Someone thought it was a good idea to try to
ride along on this success. Now we are stuck with the name.

{{index ECMAScript, compatibility}}

After its adoption outside of Netscape, a ((standard)) document was
written to describe the way the JavaScript language should work, so
that the various pieces of software that claimed to support JavaScript
were actually talking about the same language. This is called the
ECMAScript standard, after the Ecma International organization that
did the standardization. In practice, the terms ECMAScript and
JavaScript can be used interchangeably—they are two names for the same
language.

{{index [JavaScript, "weaknesses of"], debugging}}

There are those who will say _terrible_ things about the JavaScript
language. Many of these things are true. When I was required to write
something in JavaScript for the first time, I quickly came to despise
it. It would accept almost anything I typed but interpret it in a way
that was completely different from what I meant. This had a lot to do
with the fact that I did not have a clue what I was doing, of course,
but there is a real issue here: JavaScript is ridiculously liberal in
what it allows. The idea behind this design was that it would make
programming in JavaScript easier for beginners. In actuality, it
mostly makes finding problems in your programs harder because the
system will not point them out to you.

{{index [JavaScript, "flexibility of"], flexibility}}

This flexibility also has its advantages, though. It leaves space for
a lot of techniques that are impossible in more rigid languages, and
as you will see (for example in [Chapter ?](modules)) it can be used
to overcome some of JavaScript's shortcomings. After ((learning)) the
language properly and working with it for a while, I have learned to
actually _like_ JavaScript.

{{index future, [JavaScript, "versions of"], ECMAScript, "ECMAScript 6"}}

There have been several versions of JavaScript. ECMAScript version 3
was the widely supported version in the time of JavaScript's ascent to
dominance, roughly between 2000 and 2010. During this time, work was
underway on an ambitious version 4, which planned a number of radical
improvements and extensions to the language. Changing a living, widely
used language in such a radical way turned out to be politically
difficult, and work on the version 4 was abandoned in 2008, leading to
the much less ambitious version 5 coming out in 2009. Then, in 2015, a
major update, including some of the ideas planned for version 4, was
made. Since then we've had new, small updates every year.

The fact that the language is evolving means that browsers have to
constantly keep up, and if you're using an older one, it may not
support every feature. The language designers are careful to not make
any changes that could break existing programs, so new browsers can
still run old programs. In this book, I will use the 2017 version of
JavaScript.

{{index [JavaScript, "uses of"]}}

Web browsers are not the only platforms on which JavaScript is used.
Some databases, such as MongoDB and CouchDB, use JavaScript as their
scripting and query language. Several platforms for desktop and server
programming, most notably the ((Node.js)) project (the subject of
[Chapter ?](node)) provide an environment for programming JavaScript
outside of the browser.

## Code, and what to do with it

{{index "reading code", "writing code"}}

Code is the text that makes up programs. Most chapters in this book
contain quite a lot of it. I believe reading code and writing ((code))
are indispensable parts of ((learning)) to program, so try to not just
glance over the examples. Read them attentively and understand them.
This may be slow and confusing at first, but I promise that you will
quickly get the hang of it. The same goes for the ((exercises)). Don't
assume you understand them until you've actually written a working
solution.

{{index interpretation}}

I recommend you try your solutions to exercises in an actual
JavaScript interpreter. That way, you'll get immediate feedback on
whether what you are doing is working, and, I hope, you'll be tempted
to ((experiment)) and go beyond the exercises.

{{if interactive

When reading this book in your browser, you can edit (and run) all
example programs by clicking them.

if}}

{{if book

{{index download, sandbox, "running code"}}

The easiest way to run the example code in the book, and to experiment
with it, is to look it up in the online version of the book at
[_eloquentjavascript.net_](https://eloquentjavascript.net/). There, you
can click any code example to edit and run it and to see the output it
produces. To work on the exercises, go to
[_eloquentjavascript.net/code_](https://eloquentjavascript.net/code),
which provides starting code for each coding exercise and allows you
to look at the solutions.

if}}

{{index "developer tools", "JavaScript console"}}

If you want to run the programs defined in this book outside of the
book's sandbox, some care is required. Many examples stand on their
own and should work in any JavaScript environment. But code in later
chapters is often written for a specific environment (the browser or
Node.js) and can run only there. In addition, many chapters define
bigger programs, and the pieces of code that appear in them depend on
each other or on external files. The
[sandbox](https://eloquentjavascript.net/code) on the website provides
links to Zip files containing all of the scripts and data files
necessary to run the code for a given chapter.

## Overview of this book

This book contains roughly three parts. The first 12 chapters discuss
the JavaScript language itself. The next seven chapters are about web
((browsers)) and the way JavaScript is used to program them. Finally,
two chapters are devoted to ((Node.js)), another environment to
program JavaScript in.

Throughout the book, there are five _project chapters_, which describe
larger example programs to give you a taste of real programming. In
order of appearance, we will work through building a [robot](robot), a
[programming language](language), a [platform game](game), a [paint
program](paint), and a [dynamic website](skillsharing).

The language part of the book starts with four chapters to introduce
the basic structure of the JavaScript language. They introduce
[control structures](program_structure) (such as the `while` word you
saw in this introduction), [functions](functions) (writing your own
building blocks), and [data structures](data). After these, you will
be able to write simple programs. Next, Chapters [?](higher_order) and
[?](object) introduce techniques to use functions and objects to write
more _abstract_ code and thus keep complexity under control.

After a [first project chapter](robot), the first part of the book
continues with chapters on [error handling and fixing](error), on
[regular expressions](regexp) (an important tool for working with
text), on [modularity](modules) (another defense against complexity),
and on [asynchronous programming](async) (dealing with events that
take time). The [second project chapter](language) concludes the first
part of the book.

The second part, Chapters [?](browser) to [?](paint), describes the
tools that browser JavaScript has access to. You'll learn to display
things on the screen (Chapters [?](dom) and [?](canvas)), respond to
user input ([Chapter ?](event)), and communicate over the network
([Chapter ?](http)). There are again two project chapters in this
part.

After that, [Chapter ?](node) describes Node.js, and [Chapter
?](skillsharing) builds a small web system using that tool.

{{if commercial

Finally, [Chapter ?](fast) describes some of the considerations that
come up when optimizing JavaScript programs for speed.

if}}

## Typographic conventions

{{index "factorial function"}}

In this book, text written in a `monospaced` font will represent
elements of programs—sometimes they are self-sufficient fragments, and
sometimes they just refer to part of a nearby program. Programs (of
which you have already seen a few), are written as follows:

```
function factorial(n) {
  if (n == 0) {
    return 1;
  } else {
    return factorial(n - 1) * n;
  }
}
```

{{index "console.log"}}

Sometimes, in order to show the output that a program produces, the
expected output is written after it, with two slashes and an arrow in
front.

```
console.log(factorial(8));
// → 40320
```

Good luck!

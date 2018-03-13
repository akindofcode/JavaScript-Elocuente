{{meta {load_files: ["code/intro.js"]}}}

# Introducción

{{quote {author: "Ellen Ullman", title: "Close to the Machine: Technophilia and its Discontents", chapter: true}

Nosotros creemos que estamos creando el sistema para nuestros propios propósitos. Creemos que lo estamos haciendo a nuestra propia imagen... Pero la computadora no es realmente como nosotros. Es una proyección de una parte muy delgada de nosotros mismos: esa porción dedicada a la lógica, el orden, la reglas y la claridad.

quote}}

Este es un libro acerca de instruir ((computadora))s. Las computadoras son tan
comunes como los destornilladores hoy en dia. Pero son bastante más complejas
que los destornilladores, y hacer que hagan la cosa precisa que tu quieres
hacer no siempre es fácil.

Si la tarea que tienes para tu computadora es común, y bien entendida,
como mostrar tu correo electrónico o funcionar como una calculadora,
puedes abrir la ((aplicación)) apropiada y ponerte a trabajar. Pero para
tareas únicas o mas abiertas, es posible que no haya una aplicación disponible.

Ahí es donde la ((programación)) podria entrar en juego. La _programación_
es el acto de construir un _programa_—un conjunto de instrucciones precisas, 
que le dicen a una computadora qué hacer. Ya que las computadoras son bestias
tontas y pedantes, la programación es fundamentalmente tediosa y frustrante.

{{index [programming, "joy of"], speed}}

Afortunadamente, si puedes superar eso, y tal vez incluso disfrutar el rigor
de pensar en términos que las máquinas tontas puedan manejar, la programación
puede ser muy gratificante. Te permite hacer en segundos, cosas que
tardarian _para siempre_ a mano. Es una forma de hacer que tu herramienta
computadora pueda hacer cosas que antes no podía hacer. Y proporciona un maravilloso
ejercicio en pensamiento abstracto.

La mayoría de la programación se realiza con ((lenguajes de programación)).
Un _lenguaje de programación_ es un lenguaje construido artificialmente
que se utiliza para instruir computadoras. Es interesante que la forma más efectiva
que hemos encontrado para comunicarnos con una computadora es bastante
parecida a la forma que usamos para comunicarnos entre nosotros.
Al igual que los lenguajes humanos, los lenguajes de computación permiten
que las palabras y oraciones se combinen de nuevas maneras,
lo que permite expresar siempre nuevos conceptos.

{{index [JavaScript, "availability of"], "casual computing"}}

En un punto, las interfaces basadas en lenguajes, como las terminales
BASIC y DOS de los años 80 y 90, eran el principal método de 
interactuar con las computadoras. Estas han sido reemplazados en gran 
parte por interfaces visuales, que son más fáciles de aprender pero que
ofrecen menos libertad. Los lenguajes de computación todavía están allí, 
si sabes dónde mirar. Uno de estos lenguajes, JavaScript, está integrado en 
todos los navegadores web modernos y, por lo tanto, está disponible en 
casi todos los dispositivos.

{{indexsee "web browser", browser}}

Este libro intentará familiarizarte lo suficiente con este lenguaje para
hacer cosas útiles y divertidas con él.

## Acerca de la programación

{{index [programming, "difficulty of"]}}

Además de explicar JavaScript, también introduciré los principios básicos
de la programación. La programación, resulta, es difícil. Las
reglas fundamentales son típicamente simples y claras. Pero los programas
construidos en base a estas reglas tienden a ser lo suficientemente
complejos como para introducir sus propias reglas y complejidad.
En una alguna manera, estás construyendo tu propio laberinto, y
es posible que te pierdas en él.

{{index learning}}

Habrá momentos en los que leer este libro se sentira terriblemente frustrante.
Si eres nuevo en la programación, habrá mucho material nuevo para
digerir. Gran parte de este material sera entonces _combinado_ en formas que
requerirán que hagas conexiones adicionales.

Depende de ti hacer el esfuerzo necesario. Cuando estes luchando
para seguir el libro, no saltes a ninguna conclusión acerca de tus propias
capacidades. Estás bien—solo tienes que seguir intentando.
Toma un descanso, vuelva a leer algún material, y asegúrate de
leer y comprender los programas de ejemplo y los ((ejercicios)). Aprender es
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
realizadas en esta misma memoria. Las analogías que intentan comparar programas
a objetos con los que estamos familiarizados tienden a fallar. Una analogía
que es superficialmente adecuada es la de una máquina—muchas partes
separadas tienden a estar involucradas, y para hacer que funcione todo,
tenemos que considerar la formas en las que estas partes se interconectan y
contribuyen a la operación de un todo.

Una ((computadora)) es una máquina construida para actuar como anfitrión de
estas máquinas inmateriales. Las computadoras por si mismas solo pueden hacer
cosas estúpidamente sencillas. La razón por la que son tan útiles es que hacen
estas cosas a una ((velocidad)) increíblemente alta. Un programa puede
combinar ingeniosamente una cantidad enorme de estas acciones simples
para realizar cosas bastante complicadas.

{{index [programming, "joy of"]}}

Un programa es un edificio de pensamiento. No cuesta construirlo, no pesa
nada, y crece fácilmente bajo nuestras manos que teclean.

Pero sin ningun cuidado, el tamaño de un programa y su ((complejidad))
crecerán sin control, confundiendo incluso a la persona que lo creó.
Mantener a los programas bajo control es el problema principal de la programación.
Cuando un programa funciona, es hermoso. El arte de la programación es la
habilidad de controlar la complejidad. Un programa excelente es moderado—hecho
simple en su complejidad.

{{index "programming style", "best practices"}}

Algunos programadores creen que esta complejidad se maneja mejor mediante
el uso de solo un pequeño conjunto de técnicas bien entendidas en sus
programas. Ellos han compuesto reglas estrictas ("mejores prácticas") que
prescriben la forma que los programas deberían tener, y se mantienen
cuidadosamente dentro de su zona pequeña y segura.

{{index experiment}}

Esto no solo es aburrido, sino que también es ineficaz. Problemas nuevos
a menudo requieren soluciones nuevas. El campo de la programación es joven y
todavía se esta desarrollando rápidamente, y es lo suficientemente variado
como para tener espacio para aproximaciones salvajemente diferentes.
Hay muchos errores terribles que realizar cuando estas diseñando un programa, así que
ve adelante y comételos para que los entiendas mejor. La idea de cómo se ve
un buen programa se desarrolla practicando, no se aprende de una lista
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
y ceros) le daban al programador un profundo sentido de ser un poderoso
mago. Y eso tiene que valer algo en términos de satisfacción laboral.

{{index memory, instruction}}

Cada línea del programa anterior contiene una sola instrucción. Podría
ser escrito en español así:

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
debajo de el, siempre y cuando la condición que se le dio se mantenga como
verdadera. Esa condición es `cuenta <= 10`, lo que significa "_cuenta_ 
es menor o igual a 10". Ya no tenemos que crear un valor temporal y 
compararlo con cero, lo cual era un detalle poco interesante. Parte del poder 
de los lenguajes de programación es que se encargan de los detalles que poseen
de poco interés para nosotros.

{{index "console.log"}}

Al final del programa, después de que el constructo `while` haya terminado,
la operación `console.log` se usa para mostrar el resultado.

{{index "sum function", "range function", abstraction, function}}

Finalmente, aquí está cómo se vería el programa si tuvieramos acceso a
las convenientes operaciones `rango` y `suma`, que
respectivamente crean una ((colección)) de números dentro de un rango y
calculan la suma de una colección de números:

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
hablar acerca de las acciones que la computadora tiene que realizar en un nivel
superior. Ayuda a omitir detalles poco interesantes, proporciona bloques
de construcción convenientes (como `while` y `console.log`), te permite
que definas tus propios bloques de construcción (como `suma` y `rango`),
y hace que esos bloques sean fáciles de componer.

## Que es JavaScript?

{{index history, Netscape, browser, "web application", JavaScript, [JavaScript, "history of"], "World Wide Web"}}

{{indexsee WWW, "World Wide Web"}}

{{indexsee Web, "World Wide Web"}}

JavaScript se introdujo en 1995 como una forma de agregar programas a las páginas web
en el navegador Netscape Navigator. El lenguaje ha sido desde entonces
adoptado por todos los otros navegadores web principales. Ha hecho que las 
aplicaciones web modernas sean posibles—aplicaciones con las que puedes interactuar
directamente, sin hacer una recarga de página para cada acción. Pero tambien es
utilizado en sitios web más tradicionales para proporcionar diversas formas de
interactividad e ingenio.

{{index Java, naming}}

Es importante tener en cuenta que JavaScript casi no tiene nada que ver con
el lenguaje de programación llamado Java. El nombre similar fue inspirado por
consideraciones de marketing, en lugar de buen juicio. Cuando JavaScript
se estaba introduciendo, el lenguaje Java estaba siendo fuertemente publicitado y
estaba ganando popularidad. Alguien pensó que seria una buena idea intentar
cabalgar sobre este éxito. Ahora estamos atrapados con el nombre.

{{index ECMAScript, compatibility}}

Después de su adopción fuera de Netscape, un documento ((estándar)) fue
escrito para describir la forma en que debería funcionar el lenguaje JavaScript, 
para que las diversas piezas de software que decian ser compatibles con JavaScript
en realidad estuvieran hablando del mismo idioma. Este se llamo el
Estándar ECMAScript, después de la organización Ecma International que
hizo la estandarización. En la práctica, los términos ECMAScript y
JavaScript se puede usar indistintamente—son dos nombres para el mismo
idioma.

{{index [JavaScript, "weaknesses of"], debugging}}

Hay quienes dirán cosas _terribles_ sobre el lenguaje JavaScript. 
Muchas de estas cosas son verdaderas. Cuando estaba comenzando a escribir
algo en JavaScript por primera vez, rápidamente comencé a despreciarlo. 
El lenguaje aceptaba casi cualquier cosa que escribiera, pero la interpretaba 
de una manera que era completamente diferente de lo que queria decir.
Por supuesto, esto tenía mucho que ver con el hecho de que no tenía idea de 
lo que estaba haciendo, pero hay un problema real aquí: JavaScript es 
ridículamente liberal en lo que permite. La idea detrás de este diseño era que haría
a la programación en JavaScript más fácil para los principiantes. En realidad,
lo que mas hace es que encontrar problemas en tus programas sea más difícil 
porque el sistema no los señalará por ti.

{{index [JavaScript, "flexibility of"], flexibility}}

Sin embargo, esta flexibilidad también tiene sus ventajas. Deja espacio para
muchas técnicas que son imposibles en idiomas más rígidos, y
como veras (por ejemplo en el [Capítulo 10](modulos)) se pueden usar
para superar algunas de las deficiencias de JavaScript. Después de
((aprender)) el idioma correctamente y luego de trabajar con el por un tiempo, 
he aprendido a _querer_ a JavaScript.

{{index future, [JavaScript, "versions of"], ECMAScript, "ECMAScript 6"}}

Han habido varias versiones de JavaScript. ECMAScript versión 3
fue la versión mas ampliamente compatible en el momento del ascenso de JavaScript a
su dominio, aproximadamente entre 2000 y 2010. Durante este tiempo, se trabajo
en marcha hacia una ambiciosa versión 4, que planeaba una serie de mejoras 
radicales y extensiones al lenguaje. Cambiar un lenguaje vivo y ampliamente
utilizado de una manera tan radical resultó ser políticamente
difícil, y el trabajo en la versión 4 fue abandonado en 2008, lo que llevó a
la versión 5 mucho menos ambiciosa que saldria en el 2009. Luego, en 2015, una
actualización importante, incluyendo algunas de las ideas planificadas para la 
versión 4, fue realizada. 
Desde entonces hemos tenido nuevas y pequeñas actualizaciones cada año.

El hecho de que el lenguaje esté evolucionando significa que los navegadores deben
mantenerse constantemente al día, y si estás usando uno más antiguo, puede que este no
soporte todas las mejoras. Los diseñadores de lenguajes tienen cuidado de no realizar
cualquier cambio que pueda romper los ya programas existentes, de manera
que los nuevos navegadores puedan todavía ejecutar programas viejos. En este libro, 
estare usando la versión 2017 de JavaScript.

{{index [JavaScript, "uses of"]}}

Los navegadores web no son las únicas plataformas en las que se usa JavaScript.
Algunas bases de datos, como MongoDB y CouchDB, usan JavaScript como su
lenguaje de scripting y consultas. Varias plataformas para programación de 
escritorio y servidores, más notablemente el proyecto ((Node.js)) (el tema del
[Capítulo 20](Node)) proporcionan un entorno para programar en JavaScript
fuera del navegador.

## Código, y qué hacer con él

{{index "reading code", "writing code"}}

_Código_ es el texto que compone los programas. La mayoría de los capítulos en este libro
contienen bastante de el. Creo que leer código y escribir ((código))
son partes indispensables del ((aprendizaje)) para programar, así que trata de no solo
echar un vistazo a los ejemplos. Léelos atentamente y entiéndelos.
Esto puede ser algo lento y confuso al principio, pero te prometo que rápidamente 
vas coger el truco. Lo mismo ocurre con los ((ejercicios)). No hagas la
suposición de que los entiendes hasta que hayas escrito una solución funcional
para resolverlos.

{{index interpretation}}

Te recomiendo que pruebes tus soluciones a los ejercicios en un intérprete real
de JavaScript. De esta forma, obtendrás realimentación inmediata acerca de que
si esta funcionando lo que estás haciendo, y, espero, seas tentado
a ((experimentar)) y vayas más allá de los ejercicios.

{{if interactive

Al leer este libro en tu navegador, puedes editar (y ejecutar) todos los
programas de ejemplo haciendo clic en ellos.

if}}

{{if book

{{index download, sandbox, "running code"}}

La forma más fácil de ejecutar el código de ejemplo en el libro y experimentar
con él, es buscarlo en la versión en línea del libro en
[_eloquentjavascript.net_](https://eloquentjavascript.net/). Alli
puedes hacer clic en cualquier ejemplo de código para editar y ejecutarlo 
y para ver el resultado que produce. Para trabajar en los ejercicios, ve a
[_eloquentjavascript.net/code_](https://eloquentjavascript.net/code),
que proporciona el código de inicio para cada ejercicio de programación 
y te permite ver las soluciones.

if}}

{{index "developer tools", "JavaScript console"}}

Si deseas ejecutar los programas definidos en este libro fuera de
la caja de arena del libro, se requiere cierto cuidado. Muchos ejemplos se mantienen
por si mismos y deberían de funcionar en cualquier entorno de JavaScript. 
Pero código en capítulos mas avanzados a menudo se escribe para un entorno específico (el navegador o Node.js) y solo puede ser ejecutado allí. Además, muchos capítulos definen
programas más grandes, y las piezas de código que aparecen en ellos dependen de
otras o de archivos externos. La [caja de arena](https://eloquentjavascript.net/code) 
en el sitio web proporciona enlaces a archivos Zip que contienen todos 
los scripts y archivos de datos necesarios para ejecutar el código de
un capítulo determinado.

## Descripción general de este libro

Este libro contiene aproximadamente tres partes. Los primeros 12 capítulos discuten
el lenguaje JavaScript en sí. Los siguientes siete capítulos son acerca de los
((navegadores)) web y la forma en la que JavaScript es usado para programarlos. 
Finalmente, dos capítulos están dedicados a ((Node.js)), otro entorno en donde
programar JavaScript.

A lo largo del libro, hay cinco _capítulos de proyectos_, que describen
programas de ejemplo más grandes para darte una idea de la programación real. En
orden de aparición, trabajaremos en la construcción de un [robot](robot), un
[lenguaje de programación](lenguaje), un [juego de plataforma](juego), un 
[programa de paint](paint) y un [sitio web dinámico](skillsharing).

La parte del lenguaje del libro comienza con cuatro capítulos para presentar
la estructura básica del lenguaje de JavaScript. Estos introducen
[estrocturas de control](estructura_de_programa) (como la palabra `while`
que ya viste en esta introducción), [funciones](funciones) (escribir tus propios
bloques de construcción), y [estructuras de datos](datos). Después de estos, seras
capaz de escribir programas simples. Luego, los Capítulos 5(orden_superior) y
6(objeto) introducen técnicas para usar funciones y objetos y asi escribir
código más _abstracto_ y de manera que puedas mantener la complejidad bajo control.

Después de un [primer capítulo de proyecto](robot), la primera parte del libro
continúa con los capítulos sobre [manejo y solución de errores](error), en
[expresiones regulares](regexp) (una herramienta importante para trabajar con
texto), en [modularidad](modulos) (otra defensa contra la complejidad),
y en [programación asincrónica](async) (que se encarga de eventos que
toman tiempo). El [segundo capítulo de proyecto](lenguaje) concluye la primera
parte del libro.

La segunda parte, Capítulos 13(navegador) a 19(paint), describe las
herramientas a las que el JavaScript en un navegador tiene acceso. Aprenderás a mostrar
cosas en la pantalla (Capítulos 14(dom) y 17(canvas)), responder a
entradas de usuario ([Capitulo 15](evento)), y a comunicarte a través de la red
([Capitulo 18](http)). Hay dos capítulos de proyectos en este parte.

Después de eso, el [Capítulo 20](node) describe Node.js, y el [Capitulo 21](skillsharing) construye un pequeño sistema web usando esta herramienta.

{{if commercial

Finalmente, el [Capítulo 22](rapido) describe algunas de las consideraciones que
aparecen cuando se optimizan los programas de JavaScript para tener mas velocidad.

if}}

## Convenciones tipográficas

{{index "factorial function"}}

En este libro, el texto escrito en una fuente 'monoespaciada' representará
elementos de programas — a veces son fragmentos autosuficientes, y
a veces solo se refieren a partes de un programa cercano. Los programas (de
los que ya has visto algunos), se escriben de la siguiente manera:

```
function factorial(numero) {
  if (numero == 0) {
    return 1;
  } else {
    return factorial(numero - 1) * numero;
  }
}
```

{{index "console.log"}}

Algunas veces, para mostrar el resultado que produce un programa,
la salida esperada se escribe después de el, con dos slashes y una flecha en
frente.

```
console.log(factorial(8));
// → 40320
```

Buena suerte!

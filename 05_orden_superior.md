{{meta {load_files: ["code/scripts.js", "code/chapter/05_higher_order.js", "code/intro.js"], zip: "node/html"}}}

# Funciones de Orden Superior

{{if interactive

{{quote {author: "Master Yuan-Ma", title: "The Book of Programming", chapter: true}

Tzu-li y Tzu-ssu estaban jactándose del tamaño de sus ultimos
programas. 'Doscientas mil líneas', dijo Tzu-li, 'sin contar los
comentarios! ' Tzu-ssu respondió, 'Pssh, el mío tiene casi un *millón* 
de líneas ya.' El Maestro Yuan-Ma dijo, 'Mi mejor programa tiene quinientas
líneas.' Al escuchar esto, Tzu-li y Tzu-ssu se iluminaron.

quote}}

if}}

{{quote {author: "C.A.R. Hoare", title: "1980 ACM Turing Award Lecture", chapter: true}

{{index "Hoare, C.A.R."}}

Hay dos formas de construir un diseño de software: Una forma es
hacerlo tan simple de manera que obviamente no hayan deficiencias, y
la otra manera es hacerlo tan complicado que no hayan deficiencias
obvias.

quote}}

{{figure {url: "img/chapter_picture_5.jpg", alt: "Letters from different scripts", chapter: true}}}

{{index "program size"}}

Un programa grande es un programa costoso, y no solo por el tiempo que
se necesita para construirlo. El tamaño casi siempre involucra ((complejidad)), y
la complejidad confunde a los programadores. A su vez, los programadores 
confundidos, introducen errores en los programas. Un programa grande entonces
proporciona mucho espacio para que estos bugs se oculten, haciéndolos difíciles de
encontrar.

{{index "summing example"}}

Volvamos brevemente a los dos últimos programas de ejemplo en la
introducción. El primero es auto-contenido y solo tiene seis líneas de largo.

```
let total = 0, cuenta = 1;
while (cuenta <= 10) {
  total += cuenta;
  cuenta += 1;
}
console.log(total);
```

El segundo depende de dos funciones externas y tiene una línea de longitud.

```
console.log(suma(rango(1, 10)));
```

¿Cuál es más probable que contenga un bug?

{{index "program size"}}

Si contamos el tamaño de las definiciones de `suma` y `rango`, 
el segundo programa también es grande—incluso más grande que el primero. 
Pero aún así, argumentaria que es más probable que sea correcto.

{{index abstraction, "domain-specific language"}}

Es más probable que sea correcto porque la solución se expresa en un
((vocabulario)) que corresponde al problema que se está resolviendo. Sumar un
rango de números no se trata acerca de bucles y contadores. Se trata acerca
de rangos y sumas.

Las definiciones de este vocabulario (las funciones `suma` y `rango`)
seguirán involucrando bucles, contadores y otros detalles incidentales. Pero
ya que expresan conceptos más simples que el programa como un conjunto, 
son más fáciles de realizar correctamente.

## Abstracción

En el contexto de la programación, estos tipos de vocabularios suelen ser
llamados _((abstraccione))s_. Las abstracciones esconden detalles y nos dan la
capacidad de hablar acerca de los problemas en un nivel superior (o más abstracto).

{{index "recipe analogy", "pea soup"}}

Como una analogía, compara estas dos recetas de sopa de guisantes:

{{quote

Coloque 1 taza de guisantes secos por persona en un recipiente. Agregue agua hasta
que los guisantes esten bien cubiertos. Deje los guisantes en agua durante al menos 12
horas. Saque los guisantes del agua y pongalos en una cacerola para cocinar.
Agregue 4 tazas de agua por persona. Cubra la sartén y mantenga los guisantes
hirviendo a fuego lento durante dos horas. Tome media cebolla por persona. Cortela en
piezas con un cuchillo. Agréguela a los guisantes. Tome un tallo de apio por
persona. Cortelo en pedazos con un cuchillo. Agréguelo a los guisantes. Tome una
zanahoria por persona. Cortela en pedazos. ¡Con un cuchillo! Agregarla a los
guisantes. Cocine por 10 minutos más.

quote}}

Y la segunda receta:

{{quote

Por persona: 1 taza de guisantes secos, media cebolla picada, un tallo de
apio y una zanahoria.

Remoje los guisantes durante 12 horas. Cocine a fuego lento durante
2 horas en 4 tazas de agua (por persona). Picar y agregar verduras. 
Cocine por 10 minutos más.

quote}}

{{index vocabulary}}

La segunda es más corta y más fácil de interpretar. Pero necesitas
entender algunas palabras más relacionadas con la cocina—_remojar_,
_cocinar a fuego lento_, _picar_, y, supongo, _verduras_.

Cuando programamos, no podemos confiar en que todas las palabras que necesitaremos 
estaran esperando por nosotros en el diccionario. Por lo tanto, puedes caer 
en el patrón de la primera receta—resolviendo los pasos precisos que debe 
realizar la computadora, uno por uno, ciegos a los conceptos de orden 
superior que estos expresan.

{{index abstraction}}

En la programación, es una habilidad útil, darse cuenta cuando estás trabajando
en un nivel de abstracción demasiado bajo

## Abstrayendo la repetición

{{index array}}

Las funciones simples, como las hemos visto hasta ahora, 
son una buena forma de construir abstracciones. Pero a veces se quedan cortas.

{{index "for loop"}}

Es común que un programa haga algo una determinada cantidad de veces.
Puedes escribir un ((bucle)) `for` para eso, de esta manera:

```
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

¿Podemos abstraer "hacer algo _N_ veces" como una función? Bueno es
fácil de escribir una función que llame a `console.log` _N_ 
cantidad de veces.

```
function repetirLog(n) {
  for (let i = 0; i < n; i++) {
    console.log(i);
  }
}
```

{{index [function, "higher-order"], loop, [array, traversal], [function, "as value"]}}

{{indexsee "higher-order function", "function, higher-order"}}

Pero, ¿y si queremos hacer algo más que loggear los números?
Ya que "hacer algo" se puede representar como una función y las funciones
son solo valores, podemos pasar nuestra acción como un valor de función.

```{includeCode: "top_lines: 5"}
function repetir(n, accion) {
  for (let i = 0; i < n; i++) {
    accion(i);
  }
}

repetir(3, console.log);
// → 0
// → 1
// → 2
```

No es necesario pasar una función predefinida a `repetir`. A menudo,
desearas crear un valor de función al momento en su lugar.

```
let etiquetas = [];
repetir(5, i => {
  etiquetas.push(`Unidad ${i + 1}`);
});
console.log(etiquetas);
// → ["Unidad 1", "Unidad 2", "Unidad 3", "Unidad 4", "Unidad 5"]
```

{{index "loop body", "curly braces"}}

Esto está estructurado un poco como un bucle 'for'—primero describe el
tipo de bucle, y luego da un cuerpo. Sin embargo, el cuerpo ahora está escrito
como un valor de función, que está envuelto en el ((paréntesis)) de la
llamada a `repetir`. Por eso es que tiene que cerrarse con el corchete de cierre
_y_ paréntesis de cierre. En casos como este ejemplo, donde el
cuerpo es una expresión pequeña y única, podrias tambien omitir las
llaves y escribir el bucle en una sola línea.

## Funciones de orden superior

{{index [function, "higher-order"], [function, "as value"]}}

Las funciones que operan en otras funciones, ya sea tomándolas como
argumentos o retornandolas, se denominan _funciones de orden superior_.
Como ya hemos visto que las funciones son valores regulares, no existe
nada particularmente notable sobre el hecho de que tales funciones
existen. El término proviene de las ((matemáticas)), donde la distinción
entre funciones y otros valores se toma más en serio.

{{index abstraction}}

Las funciones de orden superior nos permiten abstraer sobre _acciones_, 
no solo sobre valores. Estas vienen en varias formas. Por ejemplo, puedes tener
funciones que crean nuevas funciones.

```
function mayorQue(n) {
  return m => m > n;
}
let mayorQue10 = mayorQue(10);
console.log(mayorQue10(11));
// → true
```

Y puedes tener funciones que cambien otras funciones.

```
function ruidosa(funcion) {
  return (...argumentos) => {
    console.log("llamando con", argumentos);
    let resultado = funcion(...argumentos);
    console.log("llamada con", argumentos, ", retorno", resultado);
    return resultado;
  };
}
ruidosa(Math.min)(3, 2, 1);
// → llamando con [3, 2, 1]
// → llamada con [3, 2, 1] , retorno 1
```

Incluso puedes escribir funciones que proporcionen nuevos tipos de 
((flujo de control)).

```
function aMenosQue(prueba, entonces) {
  if (!prueba) entonces();
}

repetir(3, n => {
  aMenosQue(n % 2 == 1, () => {
    console.log(n, "es par");
  });
});
// → 0 es par
// → 2 es par
```

{{index [array, methods], [array, iteration], "forEach method"}}

Hay un método de array incorporado, `forEach` que proporciona algo
como un bucle `for`/`of` como una función de orden superior.

```
["A", "B"].forEach(letra => console.log(letra));
// → A
// → B
```

## Codigo de conjunto de datos 

Un área donde brillan las funciones de orden superior es en el 
procesamiento de datos. Para procesar datos, necesitaremos algunos datos reales. 
Este capítulo usara un ((conjunto de datos)) sobre codigos—((sistema de escritura))s 
como Latin, Cirílico, o Arábico.

Recuerdas ((Unicode)) del [Capítulo 1](valores#unicode), el sistema que
asigna un número a cada carácter en el lenguaje escrito. La mayoría de estos
carácteres están asociados a un código específico. El estandar
contiene 140 codigos diferentes. 81 de los cuales todavía están en uso hoy, 59
son históricos.

Aunque solo puedo leer con fluidez los caracteres latinos, aprecio el
hecho de que las personas estan escribiendo textos en al menos 80 diferentes
sistemas de escritura, muchos de los cuales ni siquiera reconocería. Por ejemplo, 
aquí está una muestra de escritura a mano ((Tamil)).

{{figure {url: "img/tamil.png", alt: "Tamil handwriting"}}}

{{index "SCRIPTS data set"}}

El ((conjunto de datos)) de ejemplo contiene algunos piezas de información sobre los
140 codigos definidos en Unicode. Está disponible en la [caja de arena de codificación](https://eloquentjavascript.net/code#5) para este capítulo [
([_eloquentjavascript.net/code#5_](https://eloquentjavascript.net/code#5))]{if
book} como el enlace `SCRIPTS`. El enlace contiene un array de
objetos, cada uno de los cuales describe un codigo.


```{lang: "application/json"}
{
  name: "Coptic",
  ranges: [[994, 1008], [11392, 11508], [11513, 11520]],
  direction: "ltr",
  year: -200,
  living: false,
  link: "https://en.wikipedia.org/wiki/Coptic_alphabet"
}
```

Tal objeto te dice el nombre del codigo, los rangos de Unicode
asignados a él, la dirección en la que está escrito, el
hora de origen (aproximada), si todavía está en uso, y un enlace a
más información. La dirección puede ser `"ltr"` (left-to-right) para de izquierda a derecha , 
`"rtl"` (right-to-left) para de derecha a izquierda (la forma en que se escriben los textos en árabe y en hebreo), o
`"ttb"` (top-to-bottom) para de arriba a abajo (como con la escritura de Mongolia).

{{index "slice method"}}

La propiedad `ranges` contiene un array de ((rango))s de caracteres Unicode, 
cada uno de los cuales es un array de dos elementos que contiene límites inferior 
y superior. Se asignan los códigos de caracteres dentro de estos rangos
al codigo. El ((limite)) más bajo es inclusivo (el código 994 es un carácter Copto) 
y el límite superior es no-inclusivo (el código 1008 no lo es).

## Filtering arrays

{{index [array, methods], [array, filtering], "filter method", [function, "higher-order"], "predicate function"}}

To find the scripts in the data set that are still in use, the
following function might be helpful. It filters out the elements in an
array that don't pass a test.

```
function filter(array, test) {
  let passed = [];
  for (let element of array) {
    if (test(element)) {
      passed.push(element);
    }
  }
  return passed;
}

console.log(filter(SCRIPTS, script => script.living));
// → [{name: "Adlam", …}, …]
```

{{index [function, "as value"], [function, application]}}

The function uses the argument named `test`, a function value, to fill
a "gap" in the computation—the process of deciding which elements to
collect.

{{index "filter method", "pure function", "side effect"}}

Note how the `filter` function, rather than deleting elements from the
existing array, builds up a new array with only the elements that pass
the test. This function is _pure_. It does not modify the array it is
given.

Like `forEach`, `filter` is a ((standard)) array method. The example
defined the function only in order to show what it does internally.
From now on, we'll use it like this instead:

```
console.log(SCRIPTS.filter(s => s.direction == "ttb"));
// → [{name: "Mongolian", …}, …]
```

## Transforming with map

{{index [array, methods], "map method"}}

Say we have an array of objects representing scripts, produced by
filtering the `SCRIPTS` array somehow. But we want an array of names,
which is easier to inspect.

{{index [function, "higher-order"]}}

The `map` method transforms an array by applying a function to all of
its elements and building a new array from the returned values. The
new array will have the same length as the input array, but its
content will have been _mapped_ to a new form by the function.

```
function map(array, transform) {
  let mapped = [];
  for (let element of array) {
    mapped.push(transform(element));
  }
  return mapped;
}

let rtlScripts = SCRIPTS.filter(s => s.direction == "rtl");
console.log(map(rtlScripts, s => s.name));
// → ["Adlam", "Arabic", "Imperial Aramaic", …]
```

Like `forEach` and `filter`, `map` is a standard array method.

## Summarizing with reduce

{{index [array, methods], "summing example", "reduce method"}}

Another common thing to do with arrays is computing a single value
from them. Our recurring example, summing a collection of numbers, is
an instance of this. Another example would be finding the script with
the most characters.

{{indexsee "fold", "reduce method"}}

{{index [function, "higher-order"], "reduce method"}}

The higher-order operation that represents this pattern is called
_reduce_ (sometimes also called _fold_). It builds a value by
repeatedly taking a single element from the array and combining it
with the previous value. When summing numbers, you'd start with the
number zero and, for each element, add that to the sum.

The parameters to `reduce` are, apart from the array, a combining
function and a start value. This function is a little less
straightforward than `filter` and `map`, so look closely.

```
function reduce(array, combine, start) {
  let current = start;
  for (let element of array) {
    current = combine(current, element);
  }
  return current;
}

console.log(reduce([1, 2, 3, 4], (a, b) => a + b, 0));
// → 10
```

{{index "reduce method", "SCRIPTS data set"}}

The standard array method `reduce`, which of course corresponds to
this function, has an added convenience. If your array contains at
least one element, you are allowed to leave off the `start` argument.
The method will take the first element of the array as its start value
and start reducing at the second element.

```
console.log([1, 2, 3, 4].reduce((a, b) => a + b));
// → 10
```

{{index maximum, "characterCount function"}}

To use `reduce` (twice) to find the script with the most characters,
we can write something like this:

```
function characterCount(script) {
  return script.ranges.reduce((count, [from, to]) => {
    return count + (to - from);
  }, 0);
}

console.log(SCRIPTS.reduce((a, b) => {
  return characterCount(a) < characterCount(b) ? b : a;
}));
// → {name: "Han", …}
```

The `characterCount` function reduces the ranges assigned to a script
by summing their sizes. Note the use of destructuring in the parameter
list of the reducer function. The second call to `reduce` then uses
this to find the largest script by repeatedly comparing two scripts
and returning the larger one.

The Han script has over 89 thousand characters assigned to it in the
Unicode standard, making it by far the biggest writing system in the
data set. Han is a script (sometimes) used for Chinese, Japanese, and
Korean text. Those languages share a lot of characters, though they
tend to write them differently. The (US based) Unicode Consortium
decided to treat them as a single writing system in order to save
character codes. This is called "Han unification" and still makes some
people very angry.

## Composability

{{index loop, maximum}}

Consider how we would have written the previous example (finding the
biggest script) without higher-order functions. The code is not that
much worse.

```{test: no}
let biggest = null;
for (let script of SCRIPTS) {
  if (biggest == null ||
      characterCount(biggest) < characterCount(script)) {
    biggest = script;
  }
}
console.log(biggest);
// → {name: "Han", …}
```

There are a few more ((binding))s, and the program is four lines
longer. But it is still very readable.

{{index "average function", composability, [function, "higher-order"], "filter method", "map method", "reduce method"}}

{{id average_function}}

Higher-order functions start to shine when you need to _compose_
operations. As an example, let's write code that finds the average
year of origin for living and dead scripts in the data set.

```
function average(array) {
  return array.reduce((a, b) => a + b) / array.length;
}

console.log(Math.round(average(
  SCRIPTS.filter(s => s.living).map(s => s.year))));
// → 1185
console.log(Math.round(average(
  SCRIPTS.filter(s => !s.living).map(s => s.year))));
// → 209
```

So the dead scripts in Unicode are, on average, older than the living
ones. This is not a terribly meaningful or surprising statistic. But I
hope you'll agree that the code used to compute it isn't hard to read.
You can see it as a pipeline: we start with all scripts, filter out
the living (or dead) ones, take the years from those, average them,
and round the result.

You could definitely also write this computation as one big ((loop)).

```
let total = 0, count = 0;
for (let script of SCRIPTS) {
  if (script.living) {
    total += script.year;
    count += 1;
  }
}
console.log(Math.round(total / count));
// → 1185
```

But it is harder to see what was being computed and how. And because
intermediate results aren't represented as coherent values, it'd be a
lot more work to extract something like `average` into a separate
function.

{{index efficiency}}

In terms of what the computer is actually doing, these two approaches
are also quite different. The first will build up new ((array))s when
running `filter` and `map`, whereas the second only computes some
numbers, doing less work. You can usually afford the readable
approach, but if you're processing huge arrays, and doing so many
times, the less abstract style might be worth the extra speed.

## Strings and character codes

{{index "SCRIPTS data set"}}

One use of the data set would be figuring out what script a piece of
text is using. Let's go through a program that does this.

Remember that each script has an array of character code ranges
associated with it. So given a character code, we could use a function
like this to find the corresponding script (if any):

{{index "some method", "predicate function", [array, methods]}}

```{includeCode: strip_log}
function characterScript(code) {
  for (let script of SCRIPTS) {
    if (script.ranges.some(([from, to]) => code >= from &&
                                           code < to)) {
      return script;
    }
  }
  return null;
}

console.log(characterScript(121));
// → {name: "Latin", …}
```

The `some` method is another higher-order function. It takes a test
function and tells you if that function returns true for any of the
elements in the array.

{{id code_units}}

But how do we get the character codes in a string?

In [Chapter ?](values) I mentioned that JavaScript ((string))s are
encoded as a sequence of 16-bit numbers. These are called _((code
unit))s_. A ((Unicode)) ((character)) code was initially supposed to
fit within such a unit (which gives you a little over 65 thousand
characters). When it became clear that wasn't going to be enough, many
people balked at the need to use more memory per character. To address
these concerns, ((UTF-16)), the format used by JavaScript strings, was
invented. It describes most common characters using a single 16-bit
code unit, but uses a pair of two such units for others.

{{index error}}

UTF-16 is generally considered a bad idea today. It seems almost
intentionally designed to invite mistakes. It's easy to write programs
that pretend code units and characters are the same thing. And if your
language doesn't use two-unit characters, that will appear to work
just fine. But as soon as someone tries to use such a program with
some less common ((Chinese characters)), it breaks. Fortunately, with
the advent of ((emoji)), everybody has started using two-unit
characters, and the burden of dealing with such problems is more
fairly distributed.

{{index [string, length], [string, indexing], "charCodeAt method"}}

Unfortunately, obvious operations on JavaScript strings, such as
getting their length through the `length` property and accessing their
content using square brackets, deal only with code units.

```{test: no}
// Two emoji characters, horse and shoe
let horseShoe = "🐴👟";
console.log(horseShoe.length);
// → 4
console.log(horseShoe[0]);
// → (Invalid half-character)
console.log(horseShoe.charCodeAt(0));
// → 55357 (Code of the half-character)
console.log(horseShoe.codePointAt(0));
// → 128052 (Actual code for horse emoji)
```

{{index "codePointAt method"}}

JavaScript's `charCodeAt` method gives you a code unit, not a full
character code. The `codePointAt` method, added later, does give a
full Unicode character. So we could use that to get characters from a
string. But the argument passed to `codePointAt` is still an index
into the sequence of code units. So to run over all characters in a
string, we'd still need to deal with the question of whether a
character takes up one or two code units.

{{index "for/of loop", character}}

In the [previous chapter](data#for_of_loop), I mentioned that a
`for`/`of` loop can also be used on strings. Like `codePointAt`, this
type of loop was introduced at a time where people were acutely aware
of the problems with UTF-16. When you use it to loop over a string, it
gives you real characters, not code units.

```
let roseDragon = "🌹🐉";
for (let char of roseDragon) {
  console.log(char);
}
// → 🌹
// → 🐉
```

If you have a character (which will be a string of one or two code
units), you can use `codePointAt(0)` to get its code.

## Recognizing text

{{index "SCRIPTS data set", "countBy function", array}}

We have a `characterScript` function and a way to correctly loop over
characters. The next step would be to count the characters that belong
to each script. The following counting abstraction will be useful
there.

```{includeCode: strip_log}
function countBy(items, groupName) {
  let counts = [];
  for (let item of items) {
    let name = groupName(item);
    let known = counts.findIndex(c => c.name == name);
    if (known == -1) {
      counts.push({name, count: 1});
    } else {
      counts[known].count++;
    }
  }
  return counts;
}

console.log(countBy([1, 2, 3, 4, 5], n => n > 2));
// → [{name: false, count: 2}, {name: true, count: 3}]
```

The `countBy` function expects a collection (anything that we can loop
over with `for`/`of`) and a grouping function. It returns an array of
objects, each of which names a group and tells you the amount of
elements that were found in that group.

{{index "findIndex method", "indexOf method"}}

It uses another array method—`findIndex`. This method is somewhat like
`indexOf`, but instead of looking for a specific value, it finds the
first value for which the given function returns true. Like `indexOf`,
it returns -1 when no such element is found.

{{index "textScripts function", "Chinese characters"}}

Using `countBy`, we can write the function that tells us which scripts
are used in a piece of text.

```{includeCode: strip_log, startCode: true}
function textScripts(text) {
  let scripts = countBy(text, char => {
    let script = characterScript(char.codePointAt(0));
    return script ? script.name : "none";
  }).filter(({name}) => name != "none");

  let total = scripts.reduce((n, {count}) => n + count, 0);
  if (total == 0) return "No scripts found";

  return scripts.map(({name, count}) => {
    return `${Math.round(count * 100 / total)}% ${name}`;
  }).join(", ");
}

console.log(textScripts('英国的狗说"woof", 俄罗斯的狗说"тяв"'));
// → 61% Han, 22% Latin, 17% Cyrillic
```

{{index "characterScript function", "filter method"}}

The function first counts the characters by name, using
`characterScript` to assign them a name, and falling back to the
string `"none"` for characters that aren't part of any script. The
`filter` call drops the entry for `"none"` from the resulting array,
since we aren't interested in those characters.

{{index "reduce method", "map method", "join method", [array, methods]}}

To be able to compute ((percentage))s, we first need the total amount
of characters that belong to a script, which we can compute with
`reduce`. If no such characters are found, the function returns a
specific string. Otherwise, it transforms the counting entries into
readable strings with `map`, and then combine them with `join`.

## Summary

Being able to pass function values to other functions is a deeply
useful aspect of JavaScript. It allows us to write functions that
model computations with "gaps" in them. The code that calls these
functions can fill in the gaps by providing function values.

Arrays provide a number of useful higher-order methods. You can use
`forEach` to loop over the elements in an array. The `filter` method
returns a new array with the elements that didn't pass the ((predicate
function)) filtered out. Transforming an array by putting each element
through a function is done with `map`. You can use `reduce` to combine
all the elements in an array into a single value. The `some` method
tests whether any element matches a given predicate function. And
`findIndex` finds the position of the first element that matches a
predicate.

## Exercises

### Flattening

{{index "flattening (exercise)", "reduce method", "concat method", array}}

Use the `reduce` method in combination with the `concat` method to
"flatten" an array of arrays into a single array that has all the
elements of the original arrays.

{{if interactive

```{test: no}
let arrays = [[1, 2, 3], [4, 5], [6]];
// Your code here.
// → [1, 2, 3, 4, 5, 6]
```
if}}

### Your own loop

{{index "your own loop (example)", "for loop"}}

Write a higher-order function `loop` that provides something like a
`for` loop statement. It takes a value, a test function, an update
function, and a body function. Each iteration, it first runs the test
function on the current loop value, and stops if that returns false.
Then it calls the body function, giving it the current value. And
finally, it calls the update function to create a new value, and
starts from the beginning.

When defining the function, you can use a regular loop to do the
actual looping.

{{if interactive

```{test: no}
// Your code here.

loop(3, n => n > 0, n => n - 1, console.log);
// → 3
// → 2
// → 1
```

if}}

### Everything

{{index "predicate function", "everything (exercise)", "every method", "some method", [array, methods], "&& operator", "|| operator"}}

Analogous to the `some` method, arrays also have an `every` method.
This one returns true when the given function returns true for _every_
element in the array. In a way, `some` is a version of the `||`
operator that acts on arrays, and `every` is like the `&&` operator.

Implement `every` as a function that takes an array and a predicate
function as parameters. Write two versions, one using a loop and one
using the `some` method.

{{if interactive

```{test: no}
function every(array, test) {
  // Your code here.
}

console.log(every([1, 3, 5], n => n < 10));
// → true
console.log(every([2, 4, 16], n => n < 10));
// → false
console.log(every([], n => n < 10));
// → true
```

if}}

{{hint

{{index "everything (exercise)", "short-circuit evaluation", "return keyword"}}

Like the `&&` operator, the `every` method can stop evaluating further
elements as soon as it has found one that doesn't match. So the
loop-based version can jump out of the loop—with `break` or
`return`—as soon as it runs into an element for which the predicate
function returns false. If the loop runs to its end without finding
such an element, we know that all elements matched and we should
return true.

To build `every` on top of `some`, we can apply "((De Morgan's
laws))", which state that `a && b` equals `!(!a || !b)`. This can be
generalized to arrays, where all elements in the array match if there
is no element in the array that does not match.

hint}}

### Dominant writing direction

{{index "SCRIPTS data set", "direction (writing)", "groupBy function", "dominant direction (exercise)"}}

Write a function that computes the dominant writing direction in a
string of text. Remember that each script object has a `direction`
property that can be `"ltr"` (left-to-right), `"rtl"` (right-to-left),
or `"ttb"` (top-to-bottom).

{{index "characterScript function", "countBy function"}}

The dominant direction is the direction of a majority of the
characters which have a script associated with them. The
`characterScript` and `countBy` functions defined earlier in the
chapter are probably useful here.

{{if interactive

```{test: no}
function dominantDirection(text) {
  // Your code here.
}

console.log(dominantDirection("Hello!"));
// → ltr
console.log(dominantDirection("Hey, مساء الخير"));
// → rtl
```
if}}

{{hint

{{index "dominant direction (exercise)", "textScripts function", "filter method", "characterScript function"}}

Your solution might look a lot like the first half of the
`textScripts` example. You again have to count characters by a
criteria based on `characterScript`, and then filter out the part of
the result that refers to uninteresting (script-less characters).

{{index "reduce method"}}

Finding the direction with the highest character count can be done
with `reduce`. If it's not clear how, refer back to the example
earlier in the chapter, where `reduce` was used to find the script
with the most characters.

hint}}

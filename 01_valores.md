{{meta {docid: values}}}

# Valores, Tipos, y Operadores

{{quote {author: "Master Yuan-Ma", title: "The Book of Programming", chapter: true}

El programa se mueve debajo de la superficie de la maquina. Sin esfuerzo,
se expande y se contrae. En gran armonía, los electrones se dispersan y
se reagrupan. Las figuras en el monitor son tan solo ondas sobre el agua.
La escencia se mantiene invisible debajo de la superficie. 

quote}}

{{index "Yuan-Ma", "Book of Programming"}}

{{figure {url: "img/chapter_picture_1.jpg", alt: "A sea of bits", chapter: framed}}}

{{index "binary data", data, bit, memory}}

Dentro de la realidad de la computadora, solo existe información. 
Puedes leer información, modificar información, crear nueva 
información-pero eso que no es información, no puede ser mencionado.
Toda esta información esta almacenada en forma de largas secuencias 
de bits, y es por consecuencia fundamentalmente igual.

{{index CD, signal}}

Los bits son cualquier tipo de cosa de dos valores. Usualmente descritos
en ceros y unos. Dentro de la computadora, toman formas como cargas 
electricas altas y bajas, una señal fuerte o debil, o un punto brillante 
u opaco en la superficie de un CD. Cualquier pedazo de information discreta
puede ser reducido a una secuencia de ceros y unos y asi ser repsentado en bits.

{{index "binary number", radix, "decimal number"}}

Por ejemplo, podemos expresar el numero 13 en bits. Funciona de la misma 
manera que un numero decimal, pero en vez de 10 diferentes digitos, solo
tienes 2, y el peso de cada uno aumenta por un factor de 2 de derecha a 
izquierda. Aquí tenemos los bits que conforman el numero 13, con el peso
de cada digito mostrado debajo:

```{lang: null}
   0   0   0   0   1   1   0   1
 128  64  32  16   8   4   2   1
```

Entonces ese es el numero binario 00001101, o 8 + 4 + 1, o 13.

## Values

{{index memory, "volatile data storage", "hard drive"}}

Imagina un mar de bits. Un oceano de ellos. Una computadora moderna 
tradicional tiene mas de 30 billones de bits en su almacenamiento 
volatil (memoria volatil). Almacenamiento no volatil (disco duro o equivalente)
tiende a tener unas cuantas mas ordened de magnitud. 

Para poder trabajar con tales cantidades de bits sin perdernos,
debemos separarlos en porciones que representen pedazos de información.
En el entorno de JavaScript, esas porciones se llaman valores. Aunque todos 
los valores están hechos de bits, juegan un papel diferente. Cada valor
tiene un tipo que determina su rol. Algunos valores son numeros, otros
son porciones de texto, otros son funciones, y asi sucesivamente.

{{index "garbage collection"}}

Para crear un valor, solo debemos de invocar su nombre. Esto es
conveniente. No tenemos que recopilar materiales de contruccion para nuestros
valores, o pagar por ellos. Solo llamamos su nombre, y _woosh_, lo tenemos.
No son realmente creados de la nada, por supuesto. Cada valor tiene que estar
almacenado en algun sitio, y si quieres usar una cantidad gigante de ellos al
mismo tiempo, puede que te quedes sin memoria. Afortunadamente esto es un 
problema solamente si los necesitas todos al mismo tiempo. Tan pronto como 
no utilizes un valor, se disipará, dejando atrás sus bits para ser reciclados
como material de construccion para la proxima generación de valores. 

Este capitulo introduce los elementos atomicos de programas JavaScript.
Esto es, los tipos de valores simples y los operadores que actuan en 
tales valores.

## Numbers

{{index syntax, number, [number, notation]}}

Valores del tipo _numero_ son, como es de esperar, valores numericos. 
En un programa JavaScript, se escriben de la siguiente manera:

```
13
```

{{index "binary number"}}

Utiliza eso en un programa, y ocasionara que el patron de bits
que representa el numero 13 sea creado dentro de la memoria del computador.

{{index [number, representation], bit}}

JavaScript utiliza un numero fijo de bits, especificamente 64 de ellos,
para almacenar un solo valor numerico. Solo existen una cantidad finita de 
patrones que podemos crear con 64 bits, lo que significa que la cantidad de
numeros diferentes que pueden ser representados es limitada. Para una 
cantidad de _N_ digitos decimales, la cantidad de numeros que pueden ser
representados es 10^N^. Similarmente, dados 64 digitos binarios, podemos 
representar 2^64^ numeros diferentes, lo que es alrededor de 18 quintillónes
(un 18 con 18 ceros despues). Esto es muchisimo.

La memoria de un computados solia ser mucho mas pequeña que en la actualidad,
y las personas tendian a utilizar grupos de 8 o 16 bits para representar sus 
numeros. Era común accidentalmente _((desbordar))_ esta limitacion, y terminar
con un numero que no cupiera dentro de la cantidad dada de bits. Hoy en día, 
aún computadoras que caben en nuestro bolsillo tienen abundante memoria, por tanto
somos libres de usar pedazos de memoria de 64 bits, y no nos tenemos que preocupar 
por desbordamiento de memoria, solamente cuando lidiamos con numeros verdaderamente
astronomicos.

{{index sign, "floating-point number", "fractional number", "sign bit"}}

A pesar de esto, no todos los numeros enteros por debajo de 18 quintillónes caben en un
numero de JavaScript. Esos bits también almacenan numeros negativos, entonces un bit
indica el signo de un numero. Un problema mayor es que números no enteros tienen tambien
que ser representados. Para hacer esto, algunos de los bits son usados para
almacenar la pocision del punto decimal. El numero entero mas grande que puede ser
almacenado está en el rango de 9 cuatrillónes (15 ceros)-lo cual es todavia placenteramente 
inmenso. 

{{index [number, notation]}}

Los numeros fraccionarios se escriben usando un punto.

```
9.81
```

{{index exponent, "scientific notation", [number, notation]}}

Para numeros muy grandes o muy pequeños, pudieramos también usar notación 
científica agregando una "e" (de "exponente"), seguida por el exponente 
del numero:

```
2.998e8
```

Eso es 2.998 × 10^8^ = 299,800,000.

{{index pi, [number, "precision of"], "floating-point number"}}

Calculaciones con numeros enteros (también llamados _((integer))s_)
mas pequeños de los anteriormente mencionados 9 cuatrillónes están
garantizadas a ser siempre precisas. Desafortunadamente, calculaciones
con numeros fraccionarios generalmente no lo son. Así como π (pi) no puede
ser precisamente expresado por un numero finito de números decimales, 
muchos numeros pierden alguna precisión cuando solo hay 64 bits disponibles
para almacenarlos. Esto es una pena, pero solo causa problemas en situaciones
especificas. Lo importante que debemos recordar es de estar conciente de esto
y tratar numeros fraccionarios como aproximaciones, y no como valores precisos. 

### Arithmetic

{{index syntax, operator, "binary operator", arithmetic, addition, multiplication}}

Lo que mayormente se hace con numeros es aritmética. Operaciones aritmeticas
como adición y multiplicación, toma dos valores numéricos y produce un nuevo
valor a raiz de lo provisto. Asi lucen en JavaScript:

```
100 + 4 * 11
```

{{index [operator, application], asterisk, "plus character", "* operator", "+ operator"}}

Los simbolos `+` y `*` son llamados _operadores_. El primero representa
adición, y el segundo representa multiplicación. Colocar un operador entre
dos valores aplicará la operacion asociada y producirá un nuevo valor. 

{{index grouping, parentheses, precedence}}

Signifíca el ejemplo "agrega 4 y 100, y multiplica el resultado por 11",
o es la multiplicación aplicada antes de la adición? Como has podido
quizas adivinar, la multiplicación sucede primero. Pero como en matematicas,
puedes cambiar esto envolviendo la adicion en parentesis.

```
(100 + 4) * 11
```

{{index "dash character", "slash character", division, subtraction, minus, "- operator", "/ operator"}}

Para sustraer, existe el operador `-`, y para dividir existe `/`.

Cuando operadores aparecen juntos sin parentesis, el orden en el cual
son aplicados es determinado por la _((precedendia))_ de los operadores.
El operador `/` tiene la misma precedencia que `*`. Lo mismo aplica para
`+` y `-`. Cuando operadores con la misma precedencia aparecen al lado 
del otro, como en `1 - 2 + 1`, son aplicados de izquierda a derecha.

Estas reglas de precedencia no son algo de lo que debieras preocuparte.
Cuando no estés seguro, solo agrega un parentesis. 

{{index "modulo operator", division, "remainder operator", "% operator"}}

Existe otro operador aritmetico que quizas no reconocerías inmediatamente.
El symbolo `%` es utilizado para representar la operación de _residuo_.
`X % Y` es el residuo de dividir `X` entre `Y`. Por ejemplo, `314 % 100`
produce `14`, y `144 % 12` produce `0`. La presedencia del residuo es la 
la misma que la multiplicación y la divición. Frecuente mente este operador
es referido como _modulo_.

### Special numbers

{{index [number, "special values"]}}

Existen 3 valores especiales en JavaScript que son considerados 
numeros pero no se comportan como numeros normales.

{{index infinity}}

Los primeros dos son `Infinity` y `-Intinity`, los cuales representan
infinidad positiva e infinidad negativa. `Infinity - 1` es todavia
`Infinity`, y asi sucesivamente. A pesar de esto, no confíes mucho 
en computaciones que dependedn en infinidades. Esto no es matematicamente 
confiable, y puede que muy rapidamente nos resulte en el proximo numero
especial: `NaN`.

{{index NaN, "not a number", "division by zero"}}

`NaN` significa "no es un numero", aunque _sea_ un valor del tipo numerico.
Obtendremos este resultado cuando, por ejemplo, tratamos de calcular
`0 / 0` (cero dividido entre cero), `Infinity - Infinity`, o cualquier 
otra cantidad de operaciones numericas que no producen un resultado
significante.

## Strings

{{indexsee "grave accent", backtick}}

{{index syntax, text, character, [string, notation], "single-quote character", "double-quote character", "quotation mark", backtick}}

El proximo tipo de dato basico es el _((string))_. Los Strings 
son usados para representar texto. Son escritos encerrando su contenido
en comillas.

```
`Debajo en el oceano`
"Descansa en el oceano"
'Flotar en el oceano'
```

Puedes usar comillas simples, comillas dobles, o comillas invertidas 
para representar strings, siempre y cuando las comillas al principio 
y al final cuncuerden. 

{{index "line break", "newline character"}}

Casi todo puede ser colocado entre comillas, y JavaScript construirá 
un valor string a partir de ello. Pero algunos caractéres son mas dificiles.
Te puedes imaginar que colocar comillas entre comillas podría ser dificil.
_Newlines_ (los caracteres que obtienes cuando presionas la tecla de Enter)
solo pueden ser incluidos cuando el string está encapsulado con comillas
invertidas (`` ` ``), los otros typos de string deben de quedarse en una 
sola linea.

{{index [escaping, "in strings"], "backslash character"}}

Para hacer posible incluir tales caracteres en un string, la siguiente 
notación es utilizada: cuando una barra invertida es encontrada dentro de
un texto entre comillas, indica que el caracter que le sigue tiene un
significado especial. Esto es referido como _escapando_ el caracter. 
Una comilla que es precedida por una barra invertida no representará
el final del string sino que formara parte del string. Cuado el 
caractér de `n` ocurre despues de la barra invertida, es representado
como un Newline (salto de linea). Similarmente, `t` despues de una barra
invertida, significa un character de tabulación.
Toma como referencia el siguiente string: 

```
"Esta es la primera linea\nY esta es la segunda"
```

El texto actual es este: 

```{lang: null}
Esta es la primera linea
Y esta es la segunda
```

Se encuentran, por supuesto, situaciones donde queremos que una barra 
invertida en un string solo sea una barra invertida, y no un carater
especial. Si dos barras invertidas prosigen una a la otra, serán
colapsadas y sólo una permanecerá en el valor resultante del string.
Asi es como el string "_Un caracter de salto de linea es escrito
así: `"`\n`"`._" puede ser expresado: 

```
Un caracter de salto de linea es escrito así: \"\\n\"."
```

{{id unicode}}

{{index [string, representation], Unicode, character}}

También strings deben de ser moldeados como una serie de bits para poder
existir dentro del computador. La forma en la que JavaScript hace esto
es basada en el estandard _((Unicode))_. Este estandar asigna un número a
todo caracter que alguna vez pudieras necesitar, incluyendo caracteres en
griego, Arabe, Japones, Armenio, y muchos más. Si tenemos un numero que 
representa cualquier caracter, un string puede ser representado por una
secuencia de números. 

{{index "UTF-16", emoji}}

Y eso es lo que hace JavaScript. Pero hay una complicación:
La representación de JavaScript usa 16 bits por número, y hay más
de 2^16^ caracteres diferentes en Unicode (aproximadamente el doble).
Entonces algúnos caracteres, como muchos emoji, necesitan ocupar el
espacio de dos caracteres en strings JavaScript.

{{index "+ operator", concatenation}}

Los strings no pueden ser divididos, multiplicados, o restados, pero
el operador `+` _puede_ ser utilizado en ellos. No los agrega, sino que 
los _concatena_-pega dos strings juntos. La siguiente línea producirá
el string `"concatenar"`:

```
"con" + "cat" + "e" + "nar"
```

Los valores string tienen un conjunto de funciones (_metodos_) asociadas,
que pueden ser usadas para ejecutar operaciones en ellos. Regresarémos
a estas en el [Capítulo ?](data#metodos).

{{index interpolation, backtick}}

Los strings escritos con una comilla simple o doble se comportan 
casi de la misma manera-salvo el tipo de comilla que necesitamos 
para escapar dentro de ellos. Strings de comillas inversas, usualmente
llamados _((plantillas literales))_, pueden realizar unos cuantos trucos
más. Fuera de permitir saltos de lineas, pueden tambien incrustar otros
valores.

```
`la mitad de 100 es ${100 / 2}`
```

Cuando escribes algo dentro de `${}` en una plantilla literal, el
resultado será computado, convertido a string, e incluido en esa
posición. El ejemplo anterior produce "_la mitad de 100 es 50_".

## Unary operators

{{index operator, "typeof operator", type}}

No todo los operadores son simbolos. Algunos se escriben como palabras.
Un ejemplo es el operador `typeof`, que produce un string con el nombre
del tipo de valor que le mandemos.

```
console.log(typeof 4.5)
// → number
console.log(typeof "x")
// → string
```

{{index "console.log", output, "JavaScript console"}}

{{id "console.log"}}

Usaremos `console.log` en los ejemplos de codigo para indicar que
lo que queremos es ver es el resultado de alguna evaluación.
Expandiremos en esto en el [proximo capitulo](program_structure).

{{index negation, "- operator", "binary operator", "unary operator"}}

Los operadores que hemos visto hasta ahora todos operaban en does valores,
pero `typeof` sola opera con un valor. Los operadores que usan dos valores
son llamados _binarios_, mientras que aquellos operadores que usan uno son
llamados _unarios_. El operador menos puede ser usado como operador binario
o como operador unario.

```
console.log(- (10 - 2))
// → -8
```

## Boolean values

{{index Boolean, operator, true, false, bit}}

Es frecuentemente util tener un valor que distigue entre solo dos
posibilidades, como "si", y "no", o "encendido" y "apagado". Para este
proposito, JavaScript tiene el tipo _Boolean_, que tiene dos valores:
verdadero (`true`) y falso (`false`) que se escriben de la misma forma.

### Comparison

{{index comparison}}

Aqui se muestra una forma de producir valores Booleanos:

```
console.log(3 > 2)
// → true
console.log(3 < 2)
// → false
```

{{index [comparison, "of numbers"], "> operator", "< operator", "greater than", "less than"}}

Los signos `>` y `<` son tradicionalmente symbolos para "mayor que"
y "menor que", respectivamente. Ambos son operadores binarios. 
Aplicarlos resulta en un valor Boolean que indica si la condicion
se cumple.

Los Strings pueden ser comparados de la misma forma.

```
console.log("Aardvark" < "Zoroaster")
// → true
```

{{index [comparison, "of strings"]}}

La forma en la que los strings son ordenados, es aproximadamente alfabetica,
aunque no realmente de la misma forma que esperaríamos ver en un diccionario:
letras mayusculas son siempre "menores que" letras minusculas, así que `"Z" < "a"`,
y caracteres no alfabéticos como `!`, `-`, y demas, son tambíen incluidos en el 
ordenamiento. Cuando comparamos strings, JavaScript evalua los caracteres 
de izquierda a derecha, comparando los codicos ((Unicode)) uno por uno.

{{index equality, ">= operator", "<= operator", "== operator", "!= operator"}}

Otros operadores similares son `>=` (mayor o igual que), `<=` (menor y igual que),
`==` (igual a), y `!=` (no igual a).

```
console.log("Irritante" != "Arañoso")
// → true
console.log("Manzana" == "Naranja")
// → false
```

{{index [comparison, "of NaN"], NaN}}

Solo hay un valor en JavaScript que no es igual a si mismo, y este es
`NaN` ("no es numero").
There is only one value in JavaScript that is not equal to itself, and
that is `NaN` ("not a number").

```
console.log(NaN == NaN)
// → false
```

`NaN` esta supuesto a denotar el resultado de una computación sin sentido,
y como tal, no es igual al resultado de ninguna _otra_ comptacion sin sentido.

### Logical operators

{{index reasoning, "logical operators"}}

Tambien existen algunas operaciones que pueden ser aplicadas a valores
Boolean. JavaScript soporta tres operadores logicos: _and_, _or_, y _not_.
Estos pueden ser usados para "razonar" balores Boolean.

{{index "&& operator", "logical and"}}

El operador `&&` representa el operador logico _and_. Es un operador
binario, y su resultado es verdadero solo si ambos de los valores
dados son verdaderos.

```
console.log(true && false)
// → false
console.log(true && true)
// → true
```

{{index "|| operator", "logical or"}}

El operador `||` representa el operador logico _or_. Lo que produce es
verdadero si cualquiera de los valores dados es verdadero.

```
console.log(false || true)
// → true
console.log(false || false)
// → false
```

{{index negation, "! operator"}}

_Not_ se escribe como un signo de exclamación (`!`). Es un operador
unario que voltea el valor dado-`!true` produce `false` y `!false`
produce `true`.

{{index precedence}}

Cuando estos operadores Boolean son mezclados con otro tipo de
operadores, no es siempre obvio cuando son necesarios los parentesis.
En la practiva, puedes usualmente manejarte bien sabiendo que de
los operadores que hemos visto hasta ahora, `||` tiene menor precedencia,
luego le sigue `&&`, luego le siguen los operadores de comparación
(`>`, `==`, y demas), y luego el resto. Este orden ha sido determinado para
que en expresiones como la siguiente, la menos cantidad de parentesis es
requerida:

```
1 + 1 == 2 && 10 * 10 > 50
```

{{index "conditional execution", "ternary operator", "?: operator", "conditional operator", "colon character", "question mark"}}

El ultimo operador logico que discutiremos no es unario, tampoco binario,
pero ternario, esto es, que opera en tres valores. Es escrito con un
signo de interrocación y dos puntos, de esta forma: 

```
console.log(true ? 1 : 2);
// → 1
console.log(false ? 1 : 2);
// → 2
```

Este es llamado el operador _condicional_ (o algunas veces simplemente
operador _ternario_ ya que solo existe uno de este tipo). El valor a la
izquierda del signo de interrogación "decide" cual de los otros dos valores
sera retornado. Cuando es verdadero, elije el valor de en medio, y cuando es
falso, el valor de la derecha.

## Empty values

{{index undefined, null}}

Existen dos valores especiales, escritos `null` y `undefined`, que son
usados para denotar la ausencia de un valor _significativo_. Son en si mismo
valores, pero no traen consigo información.

Muchos de los operadores en el lenguage que no producen un valor significativo
(veremos algunos mas adelante), producen `undefined` simplemente porque tienen
que producir _algun_ valor.

La diferencia en significado entre `undefined`y `null`es un accidente del
diseño de JavaScript, y realmente no importa la mayor parte del tiempo. 
En los casos donde realmente tendríamos que preocuparnos por estos valores, 
mayormente recomiendo tratarlos como intercambiables.

## Automatic type conversion

{{index NaN, "type coercion"}}

En la introducción, he mencionado que JavaScript trata mucho de aceptar
casi cualquier programa que le demos, aún programas que hacen cosas
extrañas. Esto es bien demostrado por la proxima expresión:

```
console.log(8 * null)
// → 0
console.log("5" - 1)
// → 4
console.log("5" + 1)
// → 51
console.log("five" * 2)
// → NaN
console.log(false == 0)
// → true
```

{{index "+ operator", arithmetic, "* operator", "- operator"}}

Cuando un operador es aplicado el tipo de valor "incorrecto", JvasScript
calladamente convertirá ese valor al tipo que necesita, utilizando una
seria de reglas que frecuentemente no dan el resultado que quisieras
o esperarías. Esto es llamado _((coherción de tipo))_. El `null`
en la primera expresión se torna `0`, y el `"5"`en la segunda expresión
se torna `5` (de string a numero). Sin embargo, en la tercera expresión,
`+` trata concatenación de string antes de adicion numerica, entonces
el `1` es convertido a `"1"` (de numero a string)

{{index "type coercion", [number, "conversion to"]}}

When something that doesn't map to a number in an obvious way (such as
`"five"` or `undefined`) is converted to a number, you get the value
`NaN`. Further arithmetic operations on `NaN` keep producing `NaN`, so
if you find yourself getting one of those in an unexpected place, look
for accidental type conversions.

{{index null, undefined, [comparison, "of undefined values"], "== operator"}}

When comparing values of the same type using `==`, the outcome is easy
to predict: you should get true when both values are the same, except
in the case of `NaN`. But when the types differ, JavaScript uses a
complicated and confusing set of rules to determine what to do. In
most cases, it just tries to convert one of the values to the other
value's type. However, when `null` or `undefined` occurs on either
side of the operator, it produces true only if both sides are one of
`null` or `undefined`.

```
console.log(null == undefined);
// → true
console.log(null == 0);
// → false
```

That behavior is often useful. When you want to test whether a value
has a real value instead of `null` or `undefined`, you can compare it
to `null` with the `==` (or `!=`) operator.

{{index "type coercion", [Boolean, "conversion to"], "=== operator", "!== operator", comparison}}

But what if you want to test whether something refers to the precise
value `false`? The rules for converting strings and numbers to Boolean
values state that `0`, `NaN`, and the empty string (`""`) count as
`false`, while all the other values count as `true`. Because of this,
expressions like `0 == false` and `"" == false` are also true. When
you do _not_ want any automatic type conversions to happen, there are
two additional operators: `===` and `!==`. The first tests whether a
value is _precisely_ equal to the other, and the second tests whether
it is not precisely equal. So `"" === false` is false as expected.

I recommend using the three-character comparison operators defensively to
prevent unexpected type conversions from tripping you up. But when you're
certain the types on both sides will be the same, there is no problem with
using the shorter operators.

### Short-circuiting of logical operators

{{index "type coercion", [Boolean, "conversion to"], operator}}

The logical operators `&&` and `||` handle values of different types
in a peculiar way. They will convert the value on their left side to
Boolean type in order to decide what to do, but depending on the
operator and the result of that conversion, they return either the
_original_ left-hand value or the right-hand value.

{{index "|| operator"}}

The `||` operator, for example, will return the value to its left when
that can be converted to true and will return the value on its right
otherwise. This has the expected effect when the values are Boolean,
and does something analogous for values of other types.

```
console.log(null || "user")
// → user
console.log("Agnes" || "user")
// → Agnes
```

{{index "default value"}}

We can use this functionality as a way to fall back on a default
value. If you have a value that might be empty, you can put `||` after
it with a replacement value. If the initial value can be converted to
false, you'll get the replacement instead.

{{index "&& operator"}}

The `&&` operator works similarly, but the other way around. When the
value to its left is something that converts to false, it returns that
value, and otherwise it returns the value on its right.

Another important property of these two operators is that the part to
their right is evaluated only when necessary. In the case of `true ||
X`, no matter what `X` is—even if it's a piece of program that does
something _terrible_—the result will be true, and `X` is never
evaluated. The same goes for `false && X`, which is false and will
ignore `X`. This is called _((short-circuit evaluation))_.

{{index "ternary operator", "?: operator", "conditional operator"}}

The conditional operator works in a similar way. Of the second and
third value, only the one that is selected is evaluated.

## Summary

We looked at four types of JavaScript values in this chapter: numbers,
strings, Booleans, and undefined values.

Such values are created by typing in their name (`true`, `null`) or
value (`13`, `"abc"`). You can combine and transform values with
operators. We saw binary operators for arithmetic (`+`, `-`, `*`, `/`,
and `%`), string concatenation (`+`), comparison (`==`, `!=`, `===`,
`!==`, `<`, `>`, `<=`, `>=`), and logic (`&&`, `||`), as well as
several unary operators (`-` to negate a number, `!` to negate
logically, and `typeof` to find a value's type) and a ternary operator
(`?:`) to pick one of two values based on a third value.

This gives you enough information to use JavaScript as a pocket
calculator, but not much more. The [next
chapter](program_structure) will start tying
these expressions together into basic programs.

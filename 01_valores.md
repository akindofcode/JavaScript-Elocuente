{{meta {docid: values}}}

# Valores, Tipos, y Operadores

{{quote {author: "Master Yuan-Ma", title: "The Book of Programming", chapter: true}

Debajo de la superficie de la máquina, el programa se mueve. Sin esfuerzo,
se expande y se contrae. En gran armonía, los electrones se dispersan y
se reagrupan. Las figuras en el monitor son tan solo ondas sobre el agua.
La esencia se mantiene invisible debajo de la superficie. 

quote}}

{{index "Yuan-Ma", "Book of Programming"}}

{{figure {url: "img/chapter_picture_1.jpg", alt: "A sea of bits", chapter: framed}}}

{{index "binary data", data, bit, memory}}

Dentro del mundo de la computadora, solo existen datos. 
Puedes leer datos, modificar datos, crear nuevos
datos—pero todo lo que no sean datos, no puede ser mencionado.
Toda estos datos están almacenados como largas secuencias 
de bits, y por lo tanto, son fundamentalmente parecidos.

{{index CD, signal}}

Los _bits_ son cualquier tipo de cosa que pueda tener dos valores, usualmente descritos
como ceros y unos. Dentro de la computadora, toman formas como cargas
eléctricas altas y bajas, una señal fuerte o débil, o un punto brillante 
u opaco en la superficie de un CD. Cualquier pedazo de información discreta
puede ser reducida a una secuencia de ceros y unos y, así ser representada en bits.

{{index "binary number", radix, "decimal number"}}

Por ejemplo, podemos expresar el numero 13 en bits. Funciona de la misma 
manera que un numero decimal, pero en vez de 10 diferentes dígitos, solo
tienes 2, y el peso de cada uno aumenta por un factor de 2 de derecha a 
izquierda. Aquí tenemos los bits que conforman el numero 13, con el peso
de cada dígito mostrado debajo:

```{lang: null}
   0   0   0   0   1   1   0   1
 128  64  32  16   8   4   2   1
```

Entonces ese es el numero binario 00001101, o 8 + 4 + 1, o 13.

## Valores

{{index memory, "volatile data storage", "hard drive"}}

Imagina un mar de bits—un océano de ellos. Una computadora moderna 
tradicional tiene mas de 30 billones de bits en su almacenamiento de datos
volátiles (memoria funcional). El almacenamiento no volátil (disco duro o equivalente)
tiende a tener unas cuantas mas ordenes de magnitud. 

Para poder trabajar con tales cantidades de bits sin perdernos,
debemos separarlos en porciones que representen pedazos de información.
En un entorno de JavaScript, esas porciones son llamadas _((valores))_. Aunque todos 
los valores están hechos de bits, estos juegan papeles diferentes. Cada valor
tiene un tipo que determina su rol. Algunos valores son números, otros
son porciones de texto, otros son funciones, y asi sucesivamente.

{{index "garbage collection"}}

Para crear un valor, solo debemos de invocar su nombre. Esto es
conveniente. No tenemos que recopilar materiales de construcción para nuestros
valores, o pagar por ellos. Solo llamamos su nombre, y _woosh_, lo tenemos.
Aunque estos no son realmente creados de la nada, por supuesto. Cada valor tiene que ser
almacenado en algún sitio, y si quieres usar una cantidad gigante de ellos al
mismo tiempo, puede que te quedes sin memoria. Afortunadamente esto es un 
problema solamente si los necesitas todos al mismo tiempo. Tan pronto como dejes
de utilizar un valor, este se disipará, dejando atrás sus bits para que estos
sean reciclados como material de construcción para la próxima generación de valores. 

Este capitulo introduce los elementos atómicos de los programas en JavaScript,
estos son, los tipos de valores simples y los operadores que actúan en 
tales valores.

## Números

{{index syntax, number, [number, notation]}}

Valores del tipo _number_ son, como es de esperar, valores numéricos. 
En un programa JavaScript, se escriben de la siguiente manera:

```
13
```

{{index "binary number"}}

Utiliza eso en un programa, y ocasionara que el patron de bits
que representa el numero 13 sea creado dentro de la memoria del computador.

{{index [number, representation], bit}}

JavaScript utiliza un numero fijo de bits, específicamente 64 de ellos,
para almacenar un solo valor numérico. Solo existen una cantidad finita de 
patrones que podemos crear con 64 bits, lo que significa que la cantidad de
números diferentes que pueden ser representados es limitada. Para una 
cantidad de _N_ dígitos decimales, la cantidad de números que pueden ser
representados es 10^N^. Del mismo modo, dados 64 dígitos binarios, podemos 
representar 2^64^ números diferentes, lo que es alrededor de 18 mil trillones
(un 18 con 18 ceros después). Esto es muchísimo.

La memoria de un computador solía ser mucho mas pequeña que en la actualidad,
y las personas tendían a utilizar grupos de 8 o 16 bits para representar sus 
números. Era común accidentalmente _((desbordar))_ esta limitación— terminando
con un numero que no cupiera dentro de la cantidad dada de bits. Hoy en día, 
incluso computadoras que cabe dentro de tu bolsillo poseen de abundante memoria, 
por lo tanto somos libres de usar pedazos de memoria de 64 bits, y solamente 
nos tenemos que preocupar por desbordamientos de memoria cuando lidiamos 
con números verdaderamente astronómicos.

{{index sign, "floating-point number", "fractional number", "sign bit"}}

A pesar de esto, no todos los números enteros por debajo de 18 mil trillones caben en un
numero de JavaScript. Esos bits también almacenan números negativos, por lo que un bit
indica el signo de un numero. Un problema mayor es que los números no enteros tienen
que ser representados también. Para hacer esto, algunos de los bits son usados para
almacenar la posición del punto decimal. El numero entero mas grande que puede ser
almacenado está en el rango de 9 trillones (15 ceros)—lo cual es todavía placenteramente 
inmenso. 

{{index [number, notation]}}

Los números fraccionarios se escriben usando un punto:

```
9.81
```

{{index exponent, "scientific notation", [number, notation]}}

Para números muy grandes o muy pequeños, pudiéramos también usar notación 
científica agregando una "e" (de "exponente"), seguida por el exponente 
del numero:

```
2.998e8
```

Eso es 2.998 × 10^8^ = 299,800,000.

{{index pi, [number, "precision of"], "floating-point number"}}

Los cálculos con números enteros (también llamados _((integer))s_)
mas pequeños a los 9 trillones anteriormente mencionados están
garantizados a ser siempre precisos. Desafortunadamente, los calculos
con números fraccionarios, generalmente no lo son. Así como π (pi) no puede
ser precisamente expresado por un numero finito de números decimales, 
muchos numeros pierden algo de precisión cuando solo hay 64 bits disponibles
para almacenarlos. Esto es una pena, pero solo causa problemas pr'acticos
en situaciones especificas. Lo importante que debemos ser consciente de estas 
limitaciones y tratar a los números fraccionarios como aproximaciones, 
no como valores precisos. 

### Aritmética

{{index syntax, operator, "binary operator", arithmetic, addition, multiplication}}

Lo que mayormente se hace con los números es aritmética. Operaciones aritméticas
tales como adición y multiplicación, toman dos valores numéricos y producen un nuevo
valor a raíz de lo provisto. Asi lucen en JavaScript:

```
100 + 4 * 11
```

{{index [operator, application], asterisk, "plus character", "* operator", "+ operator"}}

Los símbolos `+` y `*` son llamados _operadores_. El primero representa a la
adición, y el segundo representa a la multiplicación. Colocar un operador entre
dos valores aplicará la operación asociada a esos valores y producirá un nuevo valor. 

{{index grouping, parentheses, precedence}}

¿Pero el ejemplo significa "agrega 4 y 100, y multiplica el resultado por 11",
o es la multiplicación aplicada antes de la adición? Como quizás hayas
podido adivinar, la multiplicación sucede primero. Pero como en matemáticas,
puedes cambiar esto envolviendo la adición en paréntesis.

```
(100 + 4) * 11
```

{{index "dash character", "slash character", division, subtraction, minus, "- operator", "/ operator"}}

Para sustraer, existe el operador `-`, y para dividir existe `/`.

Cuando operadores aparecen juntos sin paréntesis, el orden en el cual
son aplicados es determinado por la _((precedencia))_ de los operadores.
El ejemplo muestra que la multiplicación es aplicada antes que la adición.
El operador `/` tiene la misma precedencia que `*`. Lo mismo aplica para
`+` y `-`. Cuando operadores con la misma precedencia aparecen uno al lado 
del otro, como en `1 - 2 + 1`, son aplicados de izquierda a derecha: `(1 - 2) + 1`.

Estas reglas de precedencia no son algo de lo que deberias preocuparte.
Cuando no estés seguro, solo agrega un paréntesis. 

{{index "modulo operator", division, "remainder operator", "% operator"}}

Existe otro operador aritmético que quizás no reconozcas inmediatamente.
El símbolo `%` es utilizado para representar la operación de _residuo_.
`X % Y` es el residuo de dividir `X` entre `Y`. Por ejemplo, `314 % 100`
produce `14`, y `144 % 12` produce `0`. La precedencia del residuo es la 
la misma que la de la multiplicación y la división. Frecuentemente veras
que este operador es tambien referido como _modulo_.

### Números especiales

{{index [number, "special values"]}}

Existen 3 valores especiales en JavaScript que son considerados 
números pero no se comportan como números normales.

{{index infinity}}

Los primeros dos son `Infinity` y `-Infinity`, los cuales representan
infinidad positiva e infinidad negativa. `Infinity - 1` aun es
`Infinity`, y asi sucesivamente. A pesar de esto, no confíes mucho 
en computaciones que dependan de infinidades. Esto no es matemáticamente 
confiable, y puede que muy rápidamente nos resulte en el próximo numero
especial: `NaN`.

{{index NaN, "not a number", "division by zero"}}

`NaN` significa "no es un numero" ("not a number"), 
aunque _sea_ un valor del tipo numérico.
Obtendremos este resultado cuando, por ejemplo, tratemos de calcular
`0 / 0` (cero dividido entre cero), `Infinity - Infinity`, o cualquier 
otra cantidad de operaciones numéricas que no producen un resultado
significante.

## Strings

{{indexsee "grave accent", backtick}}

{{index syntax, text, character, [string, notation], "single-quote character", "double-quote character", "quotation mark", backtick}}

El próximo tipo de dato básico es el _((string))_. Los Strings 
son usados para representar texto. Son escritos encerrando su contenido
en comillas:

```
`Debajo en el océano`
"Descansa en el océano"
'Flotar en el océano'
```

Puedes usar comillas simples, comillas dobles, o comillas invertidas 
para representar strings, siempre y cuando las comillas al principio 
y al final concuerden. 

{{index "line break", "newline character"}}

Casi todo puede ser colocado entre comillas, y JavaScript construirá 
un valor string a partir de ello. Pero algunos caracteres son mas difíciles.
Te puedes imaginar que colocar comillas entre comillas podría ser difícil.
Los _Newlines_ (los caracteres que obtienes cuando presionas la tecla de Enter)
solo pueden ser incluidos cuando el string está encapsulado con comillas
invertidas (`` ` ``), los otros tipos de string deben de mantenerse en una 
sola linea.

{{index [escaping, "in strings"], "backslash character"}}

Para hacer posible incluir tales caracteres en un string, la siguiente 
notación es utilizada: cuando una barra invertida (\) es encontrada dentro de
un texto entre comillas, indica que el carácter que le sigue tiene un
significado especial. Esto es referido como _escapando_ el carácter. 
Una comilla que es precedida por una barra invertida no representará
el final del string sino que formara parte del string. Cuando el 
carácter de `n` es precedido por una barra invertida, este se interpreta
como un Newline (salto de linea). De la mima forma, `t` después de una barra
invertida, se interpreta como un character de tabulación.
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
invertida en un string solo sea una barra invertida, y no un carácter
especial. Si dos barras invertidas prosiguen una a la otra, serán
colapsadas y sólo una permanecerá en el valor resultante del string.
Asi es como el string "_Un carácter de salto de linea es escrito
así: `"`\n`"`._" puede ser expresado: 

```
Un carácter de salto de linea es escrito así: \"\\n\"."
```

{{id unicode}}

{{index [string, representation], Unicode, character}}

También los strings deben de ser modelados como una serie de bits para poder
existir dentro del computador. La forma en la que JavaScript hace esto
es basada en el estándar _((Unicode))_. Este estándar asigna un número a
todo carácter que alguna vez pudieras necesitar, incluyendo caracteres en
Griego, Árabe, Japones, Armenio, y asi sucesivamente. Si tenemos un numero para 
representar cada carácter, un string puede ser descrito como una
secuencia de números. 

{{index "UTF-16", emoji}}

Y eso es lo que hace JavaScript. Pero hay una complicación:
La representación de JavaScript usa 16 bits por cada elemento string, en
el cual caben 2^16^ numeros diferentes. Pero Unicode define mas caracteres
que aquellos—aproximadamente el doble, en este momento.
Entonces algunos caracteres, como muchos emojis, necesitan ocupar dos
"posiciones de caracteres" en los strings de JavaScript. Volveremos a este
tema en el [Capitulo 5](orden_superior).

{{index "+ operator", concatenation}}

Los strings no pueden ser divididos, multiplicados, o substraidos, pero
el operador `+` _puede_ ser utilizado en ellos. No los agrega, sino que 
los _concatena_—pega dos strings juntos. La siguiente línea producirá
el string `"concatenar"`:

```
"con" + "cat" + "e" + "nar"
```

Los valores string tienen un conjunto de funciones (_métodos_) asociadas,
que pueden ser usadas para realizar operaciones en ellos. Regresaremos
a estas en el [Capítulo 4](data#metodos).

{{index interpolation, backtick}}

Los strings escritos con comillas simples o dobles se comportan 
casi de la misma manera—La unica diferencia es el tipo de comilla que necesitamos 
para escapar dentro de ellos. Los strings de comillas inversas, usualmente
llamados _((plantillas literales))_, pueden realizar algunos trucos
más. Mas alla de permitir saltos de lineas, pueden también incrustar otros
valores.

```
`la mitad de 100 es ${100 / 2}`
```

Cuando escribes algo dentro de `${}` en una plantilla literal, el
resultado será computado, convertido a string, e incluido en esa
posición. El ejemplo anterior produce "_la mitad de 100 es 50_".

## Operadores unarios

{{index operator, "typeof operator", type}}

No todo los operadores son simbolos. Algunos se escriben como palabras.
Un ejemplo es el operador `typeof`, que produce un string con el nombre
del tipo de valor que le demos.

```
console.log(typeof 4.5)
// → number
console.log(typeof "x")
// → string
```

{{index "console.log", output, "JavaScript console"}}

{{id "console.log"}}

Usaremos `console.log` en los ejemplos de código para indicar que
que queremos ver el resultado de alguna evaluación.
Mas acerca de esto esto en el [proximo capitulo](estructura_de_programa).

{{index negation, "- operator", "binary operator", "unary operator"}}

En los otros operadores que hemos visto hasta ahora, todos operaban en dos valores,
pero `typeof` sola opera con un valor. Los operadores que usan dos valores
son llamados operadores _binarios_, mientras que aquellos operadores que usan uno son
llamados operadores _unarios_. El operador menos puede ser usado tanto
como un operador binario o como un operador unario.

```
console.log(- (10 - 2))
// → -8
```

## Valores Boolean

{{index Boolean, operator, true, false, bit}}

Es frecuentemente util tener un valor que distingue entre solo dos
posibilidades, como "si", y "no", o "encendido" y "apagado". Para este
propósito, JavaScript tiene el tipo _Boolean_, que tiene solo dos valores:
verdadero (`true`) y falso (`false`) que se escriben de la misma forma.

### Compraración

{{index comparison}}

Aquí se muestra una forma de producir valores Booleanos:

```
console.log(3 > 2)
// → true
console.log(3 < 2)
// → false
```

{{index [comparison, "of numbers"], "> operator", "< operator", "greater than", "less than"}}

Los signos `>` y `<` son tradicionalmente símbolos para "mayor que"
y "menor que", respectivamente. Ambos son operadores binarios. 
Aplicarlos resulta en un valor Boolean que indica si la condición
se cumple.

Los Strings pueden ser comparados de la misma forma.

```
console.log("Aardvark" < "Zoroaster")
// → true
```

{{index [comparison, "of strings"]}}

La forma en la que los strings son ordenados, es aproximadamente alfabético,
aunque no realmente de la misma forma que esperaríamos ver en un diccionario:
las letras mayúsculas son siempre "menores que" las letras minúsculas, así que `"Z" < "a"`,
y caracteres no alfabéticos (como `!`, `-` y demás) son también incluidos en el 
ordenamiento. Cuando comparamos strings, JavaScript evalúa los caracteres 
de izquierda a derecha, comparando los códigos ((Unicode)) uno por uno.

{{index equality, ">= operator", "<= operator", "== operator", "!= operator"}}

Otros operadores similares son `>=` (mayor o igual que), `<=` (menor o igual que),
`==` (igual a), y `!=` (no igual a).

```
console.log("Itchy" != "Scratchy")
// → true
console.log("Manzana" == "Naranja")
// → false
```

{{index [comparison, "of NaN"], NaN}}

Solo hay un valor en JavaScript que no es igual a si mismo, y este es
`NaN` ("no es un numero").

```
console.log(NaN == NaN)
// → false
```

Se supone que `NaN` denota el resultado de una computación sin sentido,
y como tal, no es igual al resultado de ninguna _otra_ computación sin sentido.

### Operadores lógicos

{{index reasoning, "logical operators"}}

También existen algunas operaciones que pueden ser aplicadas a valores
Boolean. JavaScript soporta tres operadores lógicos: _and_, _or_, y _not_.
Estos pueden ser usados para "razonar" acerca de valores Boolean.

{{index "&& operator", "logical and"}}

El operador `&&` representa el operador lógico _and_. Es un operador
binario, y su resultado es verdadero solo si ambos de los valores
dados son verdaderos.

```
console.log(true && false)
// → false
console.log(true && true)
// → true
```

{{index "|| operator", "logical or"}}

El operador `||` representa el operador lógico _or_. Lo que produce es
verdadero si cualquiera de los valores dados es verdadero.

```
console.log(false || true)
// → true
console.log(false || false)
// → false
```

{{index negation, "! operator"}}

_Not_ se escribe como un signo de exclamación (`!`). Es un operador
unario que voltea el valor dado—`!true` produce `false` y `!false`
produce `true`.

{{index precedence}}

Cuando estos operadores Boolean son mezclados con otros tipos de
operadores, no siempre es obvio cuando son necesarios los paréntesis.
En la práctica, usualmente puedes manejarte bien sabiendo que de
los operadores que hemos visto hasta ahora, `||` tiene la menor precedencia,
luego le sigue `&&`, luego le siguen los operadores de comparación
(`>`, `==`, y demás), y luego el resto. Este orden ha sido determinado para
que en expresiones como la siguiente, la menor cantidad de paréntesis posible sea
necesaria:

```
1 + 1 == 2 && 10 * 10 > 50
```

{{index "conditional execution", "ternary operator", "?: operator", "conditional operator", "colon character", "question mark"}}

El ultimo operador lógico que discutiremos no es unario, tampoco binario,
sino _ternario_, esto es, que opera en tres valores. Es escrito con un
signo de interrogación y dos puntos, de esta forma: 

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

## Valores vacíos

{{index undefined, null}}

Existen dos valores especiales, escritos como `null` y `undefined`, que son
usados para denotar la ausencia de un valor _significativo_. Son en si mismos
valores, pero no traen consigo información.

Muchas operaciones en el lenguaje que no producen un valor significativo
(veremos algunas mas adelante), producen `undefined` simplemente porque tienen
que producir _algún_ valor.

La diferencia en significado entre `undefined` y `null` es un accidente del
diseño de JavaScript, y realmente no importa la mayor parte del tiempo. 
En los casos donde realmente tendríamos que preocuparnos por estos valores, 
mayormente recomiendo tratarlos como intercambiables.

## Conversión de tipo automática

{{index NaN, "type coercion"}}

En la Introducción, mencione que JavaScript tiende a salirse de su camino para
aceptar casi cualquier programa que le demos, incluso programas que hacen cosas
extrañas. Esto es bien demostrado por las siguientes expresiones:

```
console.log(8 * null)
// → 0
console.log("5" - 1)
// → 4
console.log("5" + 1)
// → 51
console.log("cinco" * 2)
// → NaN
console.log(false == 0)
// → true
```

{{index "+ operator", arithmetic, "* operator", "- operator"}}

Cuando un operador es aplicado el tipo de valor "incorrecto", JavaScript
calladamente convertirá ese valor al tipo que necesita, utilizando una
serie de reglas que frecuentemente no dan el resultado que quisieras
o esperarías. Esto es llamado _((coercion de tipo))_. El `null`
en la primera expresión se torna `0`, y el `"5"`en la segunda expresión
se torna `5` (de string a numero). Sin embargo, en la tercera expresión,
`+` intenta realizar una concatenación de string antes que una adición numérica, 
entonces el `1` es convertido a `"1"` (de numero a string)

{{index "type coercion", [number, "conversion to"]}}

Cuando algo que no se traduce a un numero en una manera obvia (tal como
`"cinco"` o `undefined`) es convertido a un numero, obtenemos el valor
`NaN`. Operaciones aritméticas subsecuentes con `NaN`, continúan
produciendo `NaN`, asi que si te encuentras obteniendo uno de estos en
lugares inesperados, busca por coerciones de tipo accidentales.

{{index null, undefined, [comparison, "of undefined values"], "== operator"}}

Cuando se utiliza `==` para comparar valores del mismo tipo, el desenlace
es fácil de predecir: debemos de obtener verdadero cuando ambos valores
son lo mismo, excepto en el caso de `NaN`. Pero cuando los tipos difieren,
JavaScript utiliza una serie de reglas complicadas y confusas para determinar
que hacer. En la mayoria de los casos, solo tratara de convertir uno de estos valores
al tipo del otro valor. Sin embargo, cuando `null` o `undefined` ocurren en
cualquiera de los extremos del operador, produce verdadero solo si el otro lado
es o `null` o `undefined`.

```
console.log(null == undefined);
// → true
console.log(null == 0);
// → false
```

Este comportamiento es frecuentemente util. Cuando queremos probar
si un valor tiene un valor real en vez de `null` o `undefined`, podemos
compararlos con `null` usando el operador `==` (o `!=`).

{{index "type coercion", [Boolean, "conversion to"], "=== operator", "!== operator", comparison}}

Pero que pasa si queremos probar que algo se refiere precisamente
al valor `false`? Las reglas para convertir strings y números a valores
Boolean, dice que `0`, `NaN`, y el string vació (`""`) cuentan como `false`,
mientras que todos los otros valores cuentan como `true`. Debido a esto, 
expresiones como `0 == false`, y `"" == false` son también verdaderas.
Cuando no queremos ninguna conversion de tipo automática, existen otros
dos operadores adicionales: `===` y `!==`. El primero prueba si un valor
es _precisamente_ igual al otro, y el segundo prueba si un valor no es
precisamente igual. Entonces `"" === false` es falso, como es de esperarse.

Recomiendo usar el operador de comparación de tres caracteres defensivamente
para prevenir que conversiones de tipo inesperadas te estorben. Pero cuando
estés seguro de que el tipo va a ser el mismo en ambos lados, no es problemático
utilizar los operadores cortos.

### Corto circuito de operadores lógicos

{{index "type coercion", [Boolean, "conversion to"], operator}}

Los operadores lógicos `&&` y `||`, manejan valores de diferentes tipos
de una forma peculiar. Ellos convertirán el valor en su lado izquierdo a un
tipo Boolean para decidir que hacer, pero dependiendo del operador y el
resultado de la conversión, devolverán o el valor _original_ de la izquierda
o el valor de la derecha.

{{index "|| operator"}}

El operador `||`, por ejemplo, devolverá el valor de su izquierda cuando
este puede ser convertido a verdadero y de ser lo contrario devolverá
el valor de la derecha. Esto tiene el efecto esperado cuando los valores
son Boolean, pero se comporta de forma análoga con valores de otros tipos.

```
console.log(null || "usuario")
// → usuario
console.log("Agnes" || "usuario")
// → Agnes
```

{{index "default value"}}

Podemos utilizar esta funcionalidad como una forma de recurrir a 
un valor por defecto. Si tenemos un valor que puede estar vacío,
podemos usar `||` después de este para remplazarlo con otro valor.
Si el valor inicial puede ser convertido a falso, obtendremos el
reemplazo en su lugar.
-
{{index "&& operator"}}

El operador `&&` funciona de manera similar, pero de forma opuesta.
Cuando el valor a su derecha es algo que se convierte a falso, devuelve
ese valor, y de lo contrario, devuelve el valor a su derecha.

Otra propiedad importante de estos dos operadores es que la parte
de su derecha solo es evaluada si es necesario. En el caso de
de `true || X`, no importa que sea `X`—aun si es una pieza del programa
que hace algo _terrible_—el resultado será verdadero, y `X` nunca
es evaluado. Lo mismo sucede con `false && X`, que es falso e ignorará
`X`. Esto es llamado _((evaluación de corto circuito))_.

{{index "ternary operator", "?: operator", "conditional operator"}}

El operador condicional funciona de manera similar. Del segundo y
tercer valor, solo el que es seleccionado es evaluado.

## Resumen

Observamos cuatro tipos de valores JavaScript en este capítulo: números,
textos (`strings`), Booleans, y valores indefinidos.

Tales valores son creados escribiendo su nombre (`true`, `null`)
o valor (`13`, `"abc"`). Puedes combinar y transformar valores con
operadores. Vimos operadores binarios para aritmética (`+`, `-`, `*`, `/`,
y `%`), concatenación de strings (`+`), comparaciones (`==`, `!=`, `===`, 
`!==`, `<`, `>`, `<=`, `>=`), y lógica (`&&`, `||`), así también como 
varios otros operadores unarios (`-` para negar un numero, `!` para negar
lógicamente, y `typeof` para encontrar el valor de un tipo) y un operador 
ternario (`?:`) para elegir uno de dos valores basándose en un tercer valor.

Esto te dá la información suficiente para usar JavaScript como una
calculadora de bolsillo, pero no para mucho más. El [próximo 
capitulo](estructura_de_programa) empezará a juntar estas expresiones
para formar programas básicos.

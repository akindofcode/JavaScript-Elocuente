# Funciones

{{quote {author: "Donald Knuth", chapter: true}

La gente piensa que las ciencias de la computación son el arte de los genios,
pero la realidad verdadera es lo opuesto, estas solo consisten en mucha gente
haciendo cosas que se construyen una sobre la otra, al igual que un muro
hecho de piedras pequeñas.

quote}}

{{index "Knuth, Donald"}}

{{figure {url: "img/chapter_picture_3.jpg", alt: "Hojas de helecho con forma de fractal", chapter: framed}}}

{{index function, "code structure"}}

Las funciones son el pan y la mantequilla de la programación en JavaScript.
El concepto de envolver una pieza de programa en un valor tiene muchos usos.
Esto nos da una forma de estructurar programas más grandes, de reducir la
repetición, de asociar nombres con subprogramas y de aislar estos subprogramas
entre ellos.

La aplicación más obvia de las funciones es definir nuevo
((vocabulario)). Crear nuevas palabras en prosa suele ser un mal estilo. Pero
en la programación, es indispensable.

{{index abstraction, vocabulary}}

En promedio, un tipico adulto que hable inglés tiene unas 20,000 palabras en su
vocabulario. Pocos lenguajes de programación vienen con 20,000 comandos
ya incorporados en el. Y el vocabulario que _está_ disponible tiende a ser
más precisamente definido, y por lo tanto menos flexible, que en el lenguaje
humano. Por lo tanto, nosotros por lo general _tenemos_ que introducir nuevos
conceptos para evitar repetirnos demasiado.

## Definiendo una función

{{index "square example", [function, definition]}}

Una definición de función es un ((enlace)) regular donde el valor de
el enlace es una función. Por ejemplo, este código define `cuadrado` para
referirse a una función que produce el cuadrado de un número dado:

```
const cuadrado = function(x) {
  return x * x;
};

console.log(cuadrado(12));
// → 144
```

{{indexsee braces, "curly braces"}}
{{index "curly braces", block, syntax, "function keyword", [function, body], [function, "as value"]}}

Una función se crea con una expresión que comienza con la palabra clave
`function`. Las funciones tienen un conjunto de _((parámetro))s_ (en este caso,
solo `x`) y un _cuerpo_, que contiene las declaraciones que deben ser
ejecutadas cuando se llame a la función. El cuerpo de la función de una función
creada de esta manera siempre debe estar envuelto en llaves, incluso cuando
consista en una sola ((declaración)).

{{index "power example"}}

Una función puede tener múltiples parámetros o ningún parámetro en absoluto. En
el siguiente ejemplo, `hacerSonido` no lista ningún nombre de parámetro,
mientras que `potencia` enumera dos:

```
const hacerSonido = function() {
  console.log("Pling!");
};

hacerSonido();
// → Pling!

const potencia = function(base, exponente) {
  let resultado = 1;
  for (let cuenta = 0; cuenta < exponente; cuenta++) {
    resultado *= base;
  }
  return resultado;
};

console.log(potencia(2, 10));
// → 1024
```

{{index "return value", "return keyword", undefined}}

Algunas funciones producen un valor, como `potencia` y `cuadrado`, y algunas
no, como `hacerSonido`, cuyo único resultado es un ((efecto secundario)). Una
declaración de `return` determina el valor que es retornado por la función.
Cuando control se encuentre con tal declaración, inmediatamente salta de la
función actual y da el valor retornado al código que llamó
la función. Una declaración `return` sin una expresión después de ella
hace que la función devuelva `undefined`. Funciones que no tienen una
declaración `return` en absoluto, como `hacerSonido`, similarmente retornan
`undefined`.

## Parámetros y alcances

{{index parameter, [function, application], [binding, "from parameter"]}}

Los parámetros de una función se comportan como enlaces regulares, pero sus
valores iniciales están dados por el _llamador_ de la función, no por el código
en la función en sí.

{{indexsee "top-level scope", "global scope"}}
{{index "var keyword", "global scope", [binding, global], [binding, "scope of"]}}

Cada ((enlace)) tiene un _((alcace))_, que correspone a la parte del programa
en donde el enlace es visible. Para enlaces definidos fuera de cualquier
función o bloque, el alcance es todo el programa — puedes referirte a ellos
en donde quieras. Estos son llamados _globales_.

{{index "local scope", [binding, local]}}

Pero los enlaces creados como ((parámetro))s de función o declarados dentro de
una función solo puede ser referenciados en esa función. Estos se llaman
_locales_. Cada vez que se llame a la función, se crean
nuevas instancias de estos enlaces. Esto proporciona cierto aislamiento entre
funciones — cada llamada de función actúa sobre su pequeño propio mundo (su
entorno local), y a menudo puede ser entendida sin saber mucho acerca de
qué está pasando en el entorno global.

{{index "let keyword", "const keyword", "var keyword"}}

Los enlaces declarados con `let` y `const` son, de hecho, locales al
_((bloque))_ donde esten declarados, así que si creas uno de esos
dentro de un bucle, el código antes y después del bucle no puede "verlos".
En JavaScript anterior a 2015, solo las funciones creaban nuevos alcances,
por lo que enlaces de estilo-antiguo, creados con la palabra clave `var`,
son visibles a lo largo de toda la función en la que aparecen — o en todo el
alcance global, si no están dentro de una función.

```
let x = 10;
if (true) {
  let y = 20;
  var z = 30;
  console.log(x + y + z);
  // → 60
}
// "y" no es visible desde aqui
console.log(x + z);
// → 40
```

{{index [binding, visibility]}}

Cada ((alcance)) puede "mirar afuera" hacia al alcance que lo rodee, por lo
que `x` es visible dentro del bloque en el ejemplo. La excepción es cuando
enlaces múltiples tienen el mismo nombre — en ese caso, el código solo
puede ver al enlace más interno. Por ejemplo, cuando el código dentro de la
función `dividirEnDos` se refiere a `numero`, está viendo su _propio_ `numero`,
no al `numero` global .

```
const dividirEnDos = function(numero) {
  return numero / 2;
};

let numero = 10;
console.log(dividirEnDos(100));
// → 50
```

{{id scoping}}

### Alcance anidado

{{index [nesting, "of functions"], [nesting, "of scope"], scope, "inner function", "lexical scoping"}}

JavaScript no solo distingue entre enlaces _global_ y _local_.
Bloques y funciones se pueden crear dentro de otros bloques y
funciones, produciendo múltiples grados de localidad.

{{index "landscape example"}}

Por ejemplo, esta función — que produce los ingredientes necesarios para
hacer un lote de humus — tiene otra función dentro de ella:

```
const humus = function(factor) {
  const ingrediente = function(cantidad, unidad, nombre) {
    let cantidadIngrediente = cantidad * factor;
    if (cantidadIngrediente > 1) {
      unidad += "s";
    }
    console.log(`${cantidadIngrediente} ${unidad} ${nombre}`);
  };
  ingrediente(1, "lata", "garbanzos");
  ingrediente(0.25, "taza", "tahini");
  ingrediente(0.25, "taza", "jugo de limón");
  ingrediente(1, "clavo", "ajo");
  ingrediente(2, "cucharada", "aceite de oliva");
  ingrediente(0.5, "cucharadita", "comino");
};
```

{{index [function, scope], scope}}

El código dentro de la función `ingrediente` puede ver el enlace `factor`
de la función externa. Pero sus enlaces locales, como `unidad` o
`cantidadIngrediente`, no son visibles para la función externa.

En resumen, cada alcance local puede ver también todos los alcances locales que
lo contengan. El conjunto de enlaces visibles dentro de un bloque
está determinado por el lugar de ese bloque en el texto del programa.
Todas los enlaces de los bloques _alrededor_ de el son visibles — tanto aquellos
en bloques que lo encierran y aquellos en el nivel superior del programa.
Este enfoque a la visibilidad de enlaces es llamado _((alcance léxico))_.

## Funciones como valores

{{index [function, "as value"]}}

Los ((enlace))s de función simplemente actúan como nombres para
una pieza específica del programa. Tal enlace se define una vez y nunca cambia.
Esto hace que sea fácil confundir la función y su nombre.

{{index [binding, assignment]}}

Pero los dos son diferentes. Un valor de función puede hacer todas las cosas que
otros valores pueden hacer — puedes usarlo en ((expresion))es arbitrarias, no
solo llamarlo. Es posible almacenar un valor de función en un nuevo
enlace, pasarlo como argumento a una función, y así sucesivamente.
Del mismo modo, un enlace que referencia a una función sigue siendo solo
un enlace regular y se le puede asignar un nuevo valor, asi:

```{test: no}
let lanzarMisiles = function() {
  sistemaDeMisiles.lanzar("ahora");
};
if (modoSeguro) {
lanzarMisiles = function() {/* no hacer nada */};
}
```

{{index [function, "higher-order"]}}

En el [Capitulo 5](orden_superior), discutiremos las cosas interesantes
que se pueden hacer pasando valores de función a otras funciones.

## Notación de declaración

{{index syntax, "function keyword", "square example", [function, definition], [function, declaration]}}

Hay una forma ligeramente más corta de crear un enlace de función. Cuando
la palabra clave `function` es usada al comienzo de una declaración, funciona
de una manera diferente.

```{test: wrap}
function cuadrado(x) {
  return x * x;
}
```

{{index future, "execution order"}}

Esta es una _declaración_ de función. La declaración define el enlace
`cuadrado` y lo apunta a la función dada. Esto es un poco mas facil
de escribir, y no requiere un punto y coma después de la función.

Hay una sutileza con esta forma de definir una función.

```
console.log("El futuro dice:", futuro());

function futuro() {
  return "Nunca tendras autos voladores";
}
```

Este código funciona, aunque la función esté definida _debajo_ del código
que lo usa. Las declaraciones de funciones no son parte del flujo de control
regular de arriba hacia abajo. Estas se trasladan conceptualmente a la cima
de su alcance y pueden ser utilizadas por todo el código en ese alcance. Esto es
a veces útil porque nos da la libertad de ordenar el código en una forma
que nos parezca significativa, sin preocuparnos por tener que definir todas
las funciones antes de que sean utilizadas.

## Funciones de flecha

{{index function, "arrow function"}}

Hay una tercera notación para funciones, que se ve muy diferente
de las otras. En lugar de la palabra clave `function`, usa una flecha
(`=>`) compuesta de los caracteres igual y mayor que (no debe ser
confundida con el operador igual o mayor que, que se escribe
`>=`).

```{test: wrap}
const potencia = (base, exponente) => {
  let resultado = 1;
  for (let cuenta = 0; cuenta < exponente; cuenta++) {
    resultado *= base;
  }
  return resultado;
};
```

{{index [function, body]}}

La flecha viene _después_ de la lista de parámetros, y es seguida por
el cuerpo de la función. Expresa algo así como "esta entrada (los
((parámetro))s) produce este resultado (el cuerpo)".

{{index "curly braces", "square example"}}

Cuando solo hay un nombre de parámetro, los ((paréntesis)) alrededor de
la lista de parámetros pueden ser omitidos. Si el cuerpo es una sola expresión,
en lugar de un ((bloque)) en llaves, esa expresión será retornada por parte
de la función. Estas dos definiciones de `cuadrado` hacen la misma
cosa:

```
const cuadrado1 = (x) => { return x * x; };
const cuadrado2 = x => x * x;
```

Cuando una función de flecha no tiene parámetros, su lista de parámetros es
solo un conjunto vacío de ((paréntesis)).

```
const bocina = () => {
  console.log("Toot");
};
```

{{index verbosity}}

No hay una buena razón para tener ambas funciones de flecha y
expresiones `function` en el lenguaje. Aparte de un detalle menor,
que discutiremos en [Capítulo 6](objeto), estas hacen lo mismo.
Las funciones de flecha se agregaron en 2015, principalmente para que fuera
posible escribir pequeñas expresiones de funciones de una manera menos
verbosa. Las usaremos mucho en el [Capitulo 5](orden_superior).

{{id stack}}

## La pila de llamadas

{{indexsee stack, "call stack"}}
{{index "call stack", [function, application]}}

La forma en que el control fluye a través de las funciones está algo
involucrado. Vamos a écharle un vistazo más de cerca. Aquí hay un simple
programa que hace unas cuantas llamadas de función:

```
function saludar(quien) {
  console.log("Hola " + quien);
}
saludar("Harry");
console.log("Adios");
```

{{index "control flow", "execution order", "console.log"}}

Un recorrido por este programa es más o menos así: la llamada a `saludar`
hace que el control salte al inicio de esa función (línea 2).
La función llama `console.log`, que toma el control, hace su trabajo, y
luego retorna el control a la línea 2. Allí llega al final de la
función `saludar`, por lo que vuelve al lugar que la llamó, que es la
línea 4. La línea que sigue llama a `console.log` nuevamente. Después
que esta función retorna, el programa llega a su fin.

Podríamos mostrar el flujo de control esquemáticamente de esta manera:

```{lang: null}
parte superior
   saludar
        console.log
   saludar
parte superior
   console.log
parte superior
```

{{index "return keyword", memory}}

Porque una función tiene que regresar al lugar donde fue llamada cuando
esta retorna, la computadora debe recordar el contexto de donde
sucedió la llamada. En un caso, `console.log` tiene que volver a la
función `saludar` cuando está lista. En el otro caso, vuelve al final del
programa.

El lugar donde la computadora almacena este contexto es en la _((pila de
llamadas))_. Cada vez que se llama a una función, el contexto actual es
almacenado en la parte superior de esta "pila". Cuando una función retorna,
elimina el contexto superior de la pila y lo usa para continuar la ejecución.

{{index "infinite loop", "stack overflow", recursion}}

Almacenar esta pila requiere espacio en la memoria de la computadora. Cuando
la pila crece demasiado grande, la computadora fallará con un mensaje como
"fuera de espacio de pila" o "demasiada recursividad". El siguiente código
ilustra esto haciendo una pregunta realmente difícil a la computadora, que
causara un ir y venir infinito entre las dos funciones. Mejor dicho,
_sería_ infinito, si la computadora tuviera una pila infinita. Como son
las cosas, nos quedaremos sin espacio, o "explotaremos la pila".

```{test: no}
function gallina() {
  return huevo();
}
function huevo() {
  return gallina();
}
console.log(gallina() + " vino primero.");
// → ??
```

## Argumentos Opcionales

{{index argument, [function, application]}}

El siguiente código está permitido y se ejecuta sin ningún problema:

```
function cuadrado(x) { return x * x; }
console.log(cuadrado(4, true, "erizo"));
// → 16
```

Definimos `cuadrado` con solo un ((parámetro)). Sin embargo, cuando lo llamamos
con tres, el lenguaje no se queja. Ignora los argumentos extra
y calcula el cuadrado del primero.

{{index undefined}}

JavaScript es de extremadamente mente-abierta sobre la cantidad de argumentos
que puedes pasar a una función. Si pasa demasiados, los adicionales se ignoran.
Si pasas muy pocos, a los parámetros faltantes se les asigna el valor
`undefined`.

La desventaja de esto es que es posible, incluso probable, que
accidentalmente pases la cantidad incorrecta de argumentos a las funciones.
Y nadie te contará acerca de eso.

La ventaja es que este comportamiento se puede usar para permitir que
una función sea llamada con diferentes cantidades de argumentos. Por ejemplo,
esta función `menos` intenta imitar al operador `-` actuando en uno o
dos argumentos

```
function menos(a, b) {
  if (b === undefined) return -a;
  else return a - b;
}

console.log(menos(10));
// → -10
console.log(menos(10, 5));
// → 5
```

{{id power}}
{{index "optional argument", "default value", parameter, "= operator"}}

A menudo, cuando una función te permite omitir algunos argumentos, esos
obtendran valores predeterminados cuando no se les da ninguno.
Si escribes un operador `=` después un parámetro, seguido de una expresión,
el valor de esa expresión reemplazará al argumento cuando este no es dado.

{{index "power example"}}

Por ejemplo, esta versión de `potencia` hace que su segundo argumento
sea opcional. Si este no es proporcionado, se establecerá en dos y
la función se comportará como `cuadrado`.

```{test: wrap}
function potencia(base, exponente = 2) {
  let resultado = 1;
  for (let cuenta = 0; cuenta < exponente; cuenta++) {
    resultado *= base;
  }
  return resultado;
}

console.log(potencia(4));
// → 16
console.log(potencia(2, 6));
// → 64
```

{{index "console.log"}}

En el [próximo capítulo](data#rest_parameters), veremos una forma en el
que el cuerpo de una función puede obtener una lista de todos los argumentos
que son pasados. Esto es útil porque hace posible que una función
acepte cualquier cantidad de argumentos. Por ejemplo, `console.log` hace
esto — retorna en la consola todos los valores que se le dan.

```
console.log("C", "O", 2);
// → C O 2
```

## Cierre

{{index "call stack", "local binding", [function, "as value"], scope}}

La capacidad de tratar a las funciones como valores combinado con el hecho de
que los enlaces locales se vuelven a crear cada vez que se una función es
llamada, trae a la luz una pregunta interesante ¿Qué sucede con los
enlaces locales cuando la llamada de función que los creó ya no está activa?

El siguiente código muestra un ejemplo de esto. Define una función,
`envolverValor`, que crea un enlace local. Luego devuelve una función
que accede y devuelve este enlace local.

```
function envolverValor(n) {
  let local = n;
  return () => local;
}

let envolver1 = envolverValor(1);
let envolver2 = envolverValor(2);
console.log(envolver1());
// → 1
console.log(envolver2());
// → 2
```

Esto está permitido y funciona como es de esperar — ambas instancias de
los enlaces todavía se pueden acceder. Esta situación es una buena
demostración del hecho de que los enlaces locales se crean de nuevo para
cada llamada, y que las diferentes llamadas no pueden pisotear los enlaces
locales entre sí.

Esta característica — poder hacer referencia a una instancia específica
de un enlace local en un alcance adjunto — se llama _((cierre))_.
Una función que _cierra sobre_ algunos enlaces locales se llama _un_
cierre. Este comportamiento no solo te libera de tener que preocuparte
por la duración de los enlaces pero también hace posible usar valores de
funciones en algunas formas bastante creativas.

{{index "multiplier function"}}

Con un ligero cambio, podemos convertir el ejemplo anterior en una forma de
crear funciones que multiplican por una cantidad arbitraria.

```
function multiplicador(factor) {
  return number => number * factor;
}

let doble = multiplicador(2);
console.log(doble(5));
// → 10
```

{{index [binding, "from parameter"]}}

El enlace explícito `local` del ejemplo `envolverValor` no es realmente
necesario ya que un parámetro es en sí mismo un enlace local.

{{index [function, "model of"]}}

Pensar en programas de esta manera requiere algo de práctica. Un buen modelo
mental es pensar en los valores de función como que contienen tanto el código en
su cuerpo tanto como al entorno en el que se crean. Cuando son llamadas,
el cuerpo de la función ve su entorno original, no el entorno
en el que se realiza la llamada.

En el ejemplo, se llama a `multiplicador` y esta crea un entorno en el
que su parámetro `factor` está ligado a 2. El valor de función que
regresa, el cual se almacena en `doble`, recuerda este entorno. Asi que
cuando es es llamada, multiplica su argumento por 2.

## Recursión

{{index "power example", "stack overflow", recursion, [function, application]}}

Está perfectamente bien que una función se llame a sí misma, siempre que
no lo haga tan a menudo que desborde la pila. Una función que se llama
a si misma es llamada _recursiva_. La recursión permite que algunas
funciones sean escritas en un estilo diferente. Mira, por ejemplo,
esta implementación alternativa de `potencia`:

```{test: wrap}
function potencia(base, exponente) {
  if (exponente == 0) {
    return 1;
  } else {
    return base * potencia(base, exponente - 1);
  }
}

console.log(potencia(2, 3));
// → 8
```

{{index loop, readability, mathematics}}

Esta es bastante parecida a la forma en que los matemáticos definen
la exponenciación y posiblemente describa el concepto más claramente que
la variante con el bucle. La función se llama a si misma muchas veces con
cada vez exponentes más pequeños para lograr la multiplicación repetida.

{{index [function, application], efficiency}}

Pero esta implementación tiene un problema: en las implementaciones típicas de
JavaScript, es aproximadamente 3 veces más lenta que la versión que usa un
bucle. Correr a través de un bucle simple es generalmente más barato en
terminos de memoria que llamar a una función multiples veces.

{{index optimization}}

El dilema de la velocidad versus ((elegancia)) es interesante.
Puedes verlo como una especie de compromiso entre accesibilidad-humana y
accesibilidad-maquina. Casi cualquier programa se puede hacer más
rápido haciendolo más grande y complicado. El programador tiene que
decidir sobre cual es un equilibrio apropiado.

En el caso de la función `potencia`, la versión poco elegante (con el bucle)
sigue siendo bastante simple y fácil de leer. No tiene mucho sentido
reemplazarla con la versión recursiva. A menudo, sin embargo, un programa trata
con conceptos tan complejos que renunciar a un poco de eficiencia con el fin de
hacer que el programa sea más sencillo es útil.

{{index profiling}}

Preocuparse por la eficiencia puede ser una distracción. Es otro factor más
que complica el diseño del programa, y ​​cuando estás haciendo
algo que ya es difícil, algo más de lo que preocuparse puede ser paralizante

{{index "premature optimization"}}

Por lo tanto, siempre comienza escribiendo algo que sea correcto y fácil de
comprender. Si te preocupa que sea demasiado lento — que generalmente
no lo es, ya que la mayoría del código simplemente no se ejecuta con la
suficiente frecuencia como para tomar cantidades significativas de tiempo —
puedes medir luego y mejorarlo si necesario.

{{index "branching recursion"}}

La recursión no siempre es solo una alternativa ineficiente al bucle.
Algunos problemas son realmente más fáciles de resolver con recursión que con
bucles. En la mayoría de los casos, estos son problemas que requieren explorar o
procesar varias "ramas", cada una de las cuales podría ramificarse de nuevo
en aún más ramas.

{{id recursive_puzzle}}
{{index recursion, "number puzzle example"}}

Considera este acertijo: comenzando desde el número 1 y repetidamente
agregando 5 o multiplicando por 3, una cantidad infinita de números nuevos
pueden ser producidos. ¿Cómo escribirías una función que, dado un número,
intente encontrar una secuencia de tales adiciones y multiplicaciones que
produzca ese número?

Por ejemplo, se puede llegar al número 13 multiplicando primero por 3
y luego agregando 5 dos veces, mientras que el número 15 no puede ser
alcanzado de ninguna manera.

Aquí hay una solución recursiva:

```
function encontrarSolucion(objetivo) {
  function encontrar(actual, historia) {
    if (actual == objetivo) {
      return historia;
    } else if (actual > objetivo) {
      return null;
    } else {
      return encontrar(actual + 5, `(${historia} + 5)`) ||
             encontrar(actual * 3, `(${historia} * 3)`);
    }
  }
  return encontrar(1, "1");
}

console.log(encontrarSolucion(24));
// → (((1 * 3) + 5) * 3)
```

Ten en cuenta que este programa no necesariamente encuentra la secuencia de
operaciones _mas corta_. Este está satisfecho cuando encuentra cualquier
secuencia que funcione.

Está bien si no ves cómo funciona el programa de inmediato. Vamos a trabajar
a través de él, ya que es un gran ejercicio de pensamiento recursivo.

La función interna `encontrar` es la que hace uso de la recursión real.
Esta toma dos ((argumento))s, el número actual y un string que registra cómo
se ha alcanzado este número. Si encuentra una solución, devuelve un string que
muestra cómo llegar al objetivo. Si no puede encontrar una solución
a partir de este número, retorna `null`.

{{index null, "|| operator", "short-circuit evaluation"}}

Para hacer esto, la función realiza una de tres acciones. Si el número actual
es el número objetivo, la historia actual es una forma de llegar
ese objetivo, por lo que se devuelve. Si el número actual es mayor que
el objetivo, no tiene sentido seguir explorando esta rama ya que
tanto agregar como multiplicar solo aumentará el número, por lo que
retorna `null`. Y finalmente, si aún estamos por debajo del número objetivo,
la función intenta ambos caminos posibles que comienzan desde el número actual
llamandose a sí misma dos veces, una para agregar y otra para
multiplicar. Si la primera llamada devuelve algo que no es
`null`, esta es retornada. De lo contrario, se retorna la segunda llamada,
independientemente de si produce un string o el valor `null`.

{{index "call stack"}}

Para comprender mejor cómo esta función produce el efecto que estamos
buscando, veamos todas las llamadas a `encontrar` que se hacen cuando
buscamos una solución para el número 13.


To better understand how this function produces the effect we're
looking for, let's look at all the calls to `find` that are made when
searching for a solution for the number 13.

```{lang: null}
find(1, "1")
  find(6, "(1 + 5)")
    find(11, "((1 + 5) + 5)")
      find(16, "(((1 + 5) + 5) + 5)")
        too big
      find(33, "(((1 + 5) + 5) * 3)")
        too big
    find(18, "((1 + 5) * 3)")
      too big
  find(3, "(1 * 3)")
    find(8, "((1 * 3) + 5)")
      find(13, "(((1 * 3) + 5) + 5)")
        found!
```

```{lang: null}
encontrar(1, "1")
  encontrar(6, "(1 + 5)")
    encontrar(11, "((1 + 5) + 5)")
      encontrar(16, "(((1 + 5) + 5) + 5)")
        muy grande
      encontrar(33, "(((1 + 5) + 5) * 3)")
        muy grande
    encontrar(18, "((1 + 5) * 3)")
      muy grande
  encontrar(3, "(1 * 3)")
    encontrar(8, "((1 * 3) + 5)")
      encontrar(13, "(((1 * 3) + 5) + 5)")
        ¡encontrado!
```

La indentación indica la profundidad de la pila de llamadas. La primera vez
que `encontrar` es llamada comienza llamandose a sí misma para explorar
la solución que comienza con `(1 + 5)`. Esa llamada hara uso de la recursión
aún más para explorar _cada_ solución continuada que produce un número menor
o igual a el número objetivo. Como no encuentra uno que llegue al objetivo,
retorna `null` a la primera llamada. Ahí el operador `||` genera la llamada
que explora `(1 * 3)` para que esta suceda. Esta búsqueda tiene más
suerte — su primera llamada recursiva, a través de _otra_ llamada recursiva,
encuentra al número objetivo. Esa llamada más interna devuelve un string, y
cada uno de los operadores `||` en las llamadas intermedias pasa ese string
a lo largo, en última instancia retornando la solución.

## Funciones crecientes

{{index [function, definition]}}

Hay dos formas más o menos naturales para que las funciones sean
introducidas en los programas.

{{index repetition}}

La primera es que te encuentras escribiendo código muy similar múltiples
veces. Preferiríamos no hacer eso. Tener más código significa más espacio
para que los errores se oculten y más material para leer para las personas
que intenten entender el programa. Entonces tomamos la funcionalidad repetida,
buscamos un buen nombre para ella, y la ponemos en una función.

La segunda forma es que encuentres que necesitas alguna funcionalidad que
aún no has escrito y parece que merece su propia función.
Comenzarás por nombrar a la función y luego escribirás su cuerpo.
Incluso podrías comenzar a escribir código que usa la función antes que
definas a la función en sí misma.

{{index [function, naming], [binding, naming]}}

Lo difícil que es encontrar un buen nombre para una función es una buena
indicación de cuán claro es el concepto que está tratando de envolver.
Veamos un ejemplo.

{{index "farm example"}}

Queremos escribir un programa que imprima dos números, los números de
vacas y pollos en una granja, con las palabras `Vacas` y `Pollos`
después de ellos, y ceros acolchados antes de ambos números para que
siempre tengan tres dígitos de largo.

```{lang: null}
007 Vacas
011 Pollos
```

Esto pide una función de dos argumentos. Vamos a programar.

```
function imprimirInventarioGranja(vacas, pollos) {
  let stringVaca = String(vacas);
  while (stringVaca.length < 3) {
    stringVaca = "0" + stringVaca;
  }
  console.log(`${stringVaca} Vacas`);
  let stringPollos = String(pollos);
  while (stringPollos.length < 3) {
    stringPollos = "0" + stringPollos;
  }
  console.log(`${stringPollos} Pollos`);
}
imprimirInventarioGranja(7, 11);
```

{{index ["length property", "for string"], "while loop"}}

Escribir `.length` después de una expresión de string nos dará la longitud de
dicho string Por lo tanto, los bucles `while` seguiran sumando ceros delante
del string de numeros hasta que tenga al menos tres caracteres de longitud.

¡Misión cumplida! Pero justo cuando estamos por enviar el código a la
agricultora (junto con una considerable factura), ella nos llama y nos dice
que ella también comenzó a criar cerdos, y no podríamos extender
el software para imprimir cerdos también?

{{index "copy-paste programming"}}

Claro que podemos. Pero justo cuando estamos en el proceso de copiar y pegar
esas cuatro líneas una vez más, nos detenemos y reconsideramos. Tiene que haber
una mejor manera. Aquí hay un primer intento:

```
function imprimirEtiquetaAlcochadaConCeros(numero, etiqueta) {
  let stringNumero = String(numero);
  while (stringNumero.length < 3) {
    stringNumero = "0" + stringNumero;
  }
  console.log(`${stringNumero} ${etiqueta}`);
}

function imprimirInventarioGranja(vacas, pollos, cerdos) {
  imprimirEtiquetaAlcochadaConCeros(vacas, "Vacas");
  imprimirEtiquetaAlcochadaConCeros(pollos, "Pollos");
  imprimirEtiquetaAlcochadaConCeros(cerdos, "Cerdos");
}

imprimirInventarioGranja(7, 11, 3);
```

{{index [function, naming]}}

¡Funciona! Pero ese nombre, `imprimirEtiquetaAlcochadaConCeros`, es un poco
incómodo. Combina tres cosas: impresión, alcochar con ceros y añadir
una etiqueta en una sola función.

{{index "zeroPad function"}}

En lugar de eliminar la parte repetida de nuestro programa al por mayor,
intentemos elegir un solo _concepto_.

```
function alcocharConCeros(numero, amplitud) {
  let string = String(numero);
  while (string.length < amplitud) {
    string = "0" + string;
  }
  return string;
}

function imprimirInventarioGranja(vacas, pollos, cerdos) {
  console.log(`${alcocharConCeros(vacas, 3)} Vacas`);
  console.log(`${alcocharConCeros(pollos, 3)} Pollos`);
  console.log(`${alcocharConCeros(cerdos, 3)} Cerdos`);
}

imprimirInventarioGranja(7, 16, 3);
```

{{index readability, "pure function"}}

Una función con un nombre agradable y obvio como `alcocharConCeros` hace
que sea más fácil de entender lo que hace para alguien que lee el código.
Y tal función es útil en situaciones más alla de este programa en específico.
Por ejemplo, podrías usarla para ayudar a imprimir tablas de
números de una manera alineada.

{{index [interface, design]}}

¿Que tan inteligente y versátil _deberia_ ser nuestra función? Podríamos
escribir cualquier cosa, desde una función terriblemente simple que solo
pueda alcochar un número para que tenga tres caracteres de ancho,
a un complicado sistema generalizado de formateo de números que maneje
números fraccionarios, números negativos, alineación de puntos decimales,
relleno con diferentes caracteres, y así sucesivamente.

Un principio útil es no agregar mucho ingenio a menos que estes absolutamente
seguro de que lo vas a necesitar. Puede ser tentador escribir "((framework))s"
generalizados para cada funcionalidad que encuentres.
Resiste ese impulso. No realizarás ningún trabajo real de esta manera,
solo estarás escribiendo código que nunca usarás.

{{id pure}}
## Funciones y efectos secundarios

{{index "side effect", "pure function", [function, purity]}}

Las funciones se pueden dividir aproximadamente en aquellas que se llaman
por su efectos secundarios y aquellas que son llamadas por su valor de
retorno. (Aunque definitivamente también es posible tener tanto efectos
secundarios como devolver un valor en una misma función.)

{{index reuse}}

La primera función auxiliar en el ((ejemplo de la granja)),
`imprimirEtiquetaAlcochadaConCeros`, se llama por su efecto secundario:
imprime una línea. La segunda versión, `alcocharConCeros`, se llama por su
valor de retorno. No es coincidencia que la segunda sea útil en más situaciones
que la primera. Las funciones que crean valores son más fáciles de combinar
en nuevas formas que las funciones que directamente realizan efectos
secundarios.

{{index substitution}}

Una función _pura_ es un tipo específico de función de producción-de-valores
que no solo no tiene efectos secundarios pero que tampoco depende de los
efectos secundarios de otro código — por ejemplo, no lee enlaces globales cuyos
valores pueden cambiar. Una función pura tiene la propiedad agradable de que
cuando se le llama con los mismos argumentos, siempre produce el mismo valor
(y no hace nada más). Una llamada a tal función puede ser sustituida por
su valor de retorno sin cambiar el significado del código.
Cuando no estás seguro de que una función pura esté funcionando
correctamente, puedes probarla simplemente llamándola, y saber que si
funciona en ese contexto, funcionará en cualquier contexto. Las funciones
no puras tienden a requerir más configuración para poder ser probadas.

{{index optimization, "console.log"}}

Aún así, no hay necesidad de sentirse mal cuando escribas funciones que no son
puras o de hacer una guerra santa para purgarlas de tu código.
Los efectos secundarios a menudo son útiles. No habría forma de escribir una
versión pura de `console.log`, por ejemplo, y `console.log` es bueno de tener.
Algunas operaciones también son más fáciles de expresar en una manera
eficiente cuando usamos efectos secundarios, por lo que la velocidad de
computación puede ser una razón para evitar la pureza.

## Summary

This chapter taught you how to write your own functions. The
`function` keyword, when used as an expression, can create a function
value. When used as a statement, it can be used to declare a binding
and give it a function as its value. Arrow functions are yet another
way to create functions.

```
// Create a function value f
const f = function(a) {
  console.log(a + 2);
};

// Declare g to be a function
function g(a, b) {
  return a * b * 3.5;
}

// A less verbose function value
let h = a => a % 3;
```

A key aspect in understanding functions is understanding scopes. Each
block creates a new scope. Parameters and bindings declared in a given
scope are local, and not visible from the outside. Bindings declared
with `var` behave differently—they end up in the nearest function
scope or the global scope.

Separating the tasks your program performs into different functions is
helpful. You won't have to repeat yourself as much, and functions can
help organize a program by grouping code into pieces that do specific
things.

## Exercises

### Minimum

{{index "Math object", "minimum (exercise)", "Math.min function", minimum}}

The [previous chapter](program_structure#return_values) introduced the
standard function `Math.min` that returns its smallest argument. We
can build something like that now. Write a function `min` that takes
two arguments and returns their minimum.

{{if interactive

```{test: no}
// Your code here.

console.log(min(0, 10));
// → 0
console.log(min(0, -10));
// → -10
```
if}}

{{hint

{{index "minimum (exercise)"}}

If you have trouble putting braces and
parentheses in the right place to get a valid function definition,
start by copying one of the examples in this chapter and modifying it.

{{index "return keyword"}}

A function may contain multiple `return` statements.

hint}}

### Recursion

{{index recursion, "isEven (exercise)", "even number"}}

We've seen that `%` (the remainder operator) can be used to test
whether a number is even or odd by using `% 2` to see whether it's
divisible by two. Here's another way to define whether a positive
whole number is even or odd:

- Zero is even.

- One is odd.

- For any other number _N_, its evenness is the same as _N_ - 2.

Define a recursive function `isEven` corresponding to this
description. The function should accept a single parameter (a
positive, whole number) and return a Boolean.

{{index "stack overflow"}}

Test it on 50 and 75. See how it behaves on -1. Why? Can you think of
a way to fix this?

{{if interactive

```{test: no}
// Your code here.

console.log(isEven(50));
// → true
console.log(isEven(75));
// → false
console.log(isEven(-1));
// → ??
```

if}}

{{hint

{{index "isEven (exercise)", ["if keyword", chaining], recursion}}

Your function will likely look somewhat similar to the inner `find`
function in the recursive `findSolution`
[example](functions#recursive_puzzle) in this chapter, with an
`if`/`else if`/`else` chain that tests which of the three cases
applies. The final `else`, corresponding to the third case, makes the
recursive call. Each of the branches should contain a `return`
statement or in some other way arrange for a specific value to be
returned.

{{index "stack overflow"}}

When given a negative number, the function will recurse again and
again, passing itself an ever more negative number, thus getting
further and further away from returning a result. It will eventually
run out of stack space and abort.

hint}}

### Bean counting

{{index "bean counting (exercise)", [string, indexing], "zero-based counting", ["length property", "for string"]}}

You can get the Nth character, or letter, from a string by writing
`"string"[N]`. The returned value will be a string containing only one
character (for example, `"b"`). The first character has position zero,
which causes the last one to be found at position `string.length - 1`.
In other words, a two-character string has length 2, and its
characters have positions 0 and 1.

Write a function `countBs` that takes a string as its only argument
and returns a number that indicates how many uppercase "B" characters
there are in the string.

Next, write a function called `countChar` that behaves like `countBs`,
except it takes a second argument that indicates the character that is
to be counted (rather than counting only uppercase "B" characters).
Rewrite `countBs` to make use of this new function.

{{if interactive

```{test: no}
// Your code here.

console.log(countBs("BBC"));
// → 2
console.log(countChar("kakkerlak", "k"));
// → 4
```

if}}

{{hint

{{index "bean counting (exercise)", ["length property", "for string"], "counter variable"}}

Your function will need a ((loop)) that looks at every character in
the string. It can run an index from zero to one below its length (`<
string.length`). If the character at the current position is the same
as the one the function is looking for, it adds 1 to a counter
variable. Once the loop has finished, the counter can be returned.

{{index "local binding"}}

Take care to make all the bindings used in the function _local_ to the
function by using the `let` keyword.

hint}}

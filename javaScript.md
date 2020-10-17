---
title: "Javascript"
slug: "Javascript"
description: "💛"
keywords: [programacion, desarrollo, software, javascript, js]
draft: true
tags: []
math: false
toc: false
---
# Aspectos Basicos

## Como llega y corre un script en el navegador
El **DOM** es la representación que hace el navegador de un documento HTML.

El navegador interpreta el archivo HTML y cuando termina de transformarlo al DOM se dispara el evento *DOMContentLoaded* lo que significa que todo el documento está disponible para ser manipulado.

Todo script que carguemos en nuestra página tiene un llamado y una ejecución. Hay que tener en cuenta que cuando carga una página y se encuentra un script a ejecutar toda la carga se detiene. Por eso se recomienda agregar tus scripts justo antes de cerrar el body para que todo el documento esté disponible(de esta forma puedes interactuar con los elementos del DOM con la seguridad de q ue existen).
Existen metodos asincronos para evitar que la creacion del DOM se detenga inmediatamente al leer el script. Esto tanto con *async* como *defer* podemos hacer llamados asíncronos pero tiene sus diferencias:

- **async**. Con async podemos hacer la petición de forma asíncrona y no vamos a detener la carga del DOM hasta que se haga la ejecución del código.
- **defer**. La petición es igual asíncrona como en el async pero va a deferir la ejecución del Javascript hasta el final de que se cargue todo el documento. Es decir el script corre despues de que todo el arbol del DOM es construido.


## Concatenacion

- Tradicional:
    Es la utilizada tradicionalmente en los lenguajes de programacion, funciona utilizando el operador +. Ejemplo:

    'Jesus' + 'Millan'

    \>> 'Jesus Millan'

- Interpolacion:
    Es una forma nueva de concatenar texto, y para en lo personal me parece mas facil y clara de leer. Funciona utilizando el operador comillas invertidas (` `). Ejemplo:

    var firstName = 'Jesus';
    var lastName  = 'Millan';

    \`${firstName} ${lastName}`

    \>> 'Jesus Millan'

    **NOTA:** Dentro de las {} van codigo Js, el caracter para escapar texto es '\'.

## Depurar
En ocasiones nuestro código puede fallar por errores de syntaxis o errores lógicos. En caso de que quieras verificar tu código, debes utilizar la palabra clave 'debugger'. El código se detiene cada vez que lee esta palabra.

## Diferencia entre var, let y const
- ““*var*”” es la manera más antigua de declarar variables. No es muy estricta en cuanto al alcance, ya que al declarar variables de esta forma, dichas variables podrán ser accedidas, e incluso modificaddas, tanto dentro como fuera de los bloques internos en una función.

- ““*let*”” por otra parte, el alcance se reduce al bloque (las llaves) en el cual la variable fue declarada. Fuera de este bloque la variable no existe. Una vez declarada la variable con let, no se puede volver a declarar con en ninguna otra parte de la función.

- ““*const*”” al igual que ““*let*”” se define en el contexto o alcance de un bloque, a diferencia de let y var, las varibles definidas como constantes (const), ya no podrán ser modificadas ni declaradas nuevamente, en ninguna otra parte de la función o el contexto en el que ya existen.

La recomendación es reducir siempre al mínimo el alcance de nuestras variables, por lo que se debe usar let en lugar de var mientras sea posible.

# Variables

## Strings

Son cadenas de texto. Para indicar que estamos usando una cadena de texto debemos de colocar las comillas simples ('').

### Metodos

- toUpperCase:
    Sirve para transformar un String a mayúsculas.
- toLowerCase:
    Sirve para transformar el string a minúsculas.
- charAt(N):
    Retorna el caracter que esta en la posicion N.

### Atributo

- length:
    Nos indica la cantidad de caractéres que tiene un string.
Para concatenar dos strings se utiliza el símbolo (+)
Ejemplo:
`let nombreCompleto = nombre + ’ ’ + apellido`
O carateres invertidos (`) delimitando las variables en ${}
```
let nombreCompleto =`${nombre} ${apellido}`
```

# JSON: JavaScript Object Notation
Un objeto nos permite la modelacion y abstracion de un "objeto" del mundo real.

**NOTA:** Un objeto también se puede pasar como atributo en una función.

## Definicion
Se definen delimitados mediante llaves( {} )

Un atributo se compone de una clave (key) y un valor (value), que se separan entre sí por dos puntos( : ). Los valores pueden ser de tipo *string*, *número*, *booleano*, etc. Cada atributo está separado del siguiente por una coma( , ). Un objeto puede tener todos los atributos que sean necesarios.

## Acceso

Existen al menos dos formas de acceder al valor de un atributo de un objeto:

### Comun
 Escribir el nombre de un objeto separado por un punto del nombre de un atributo.Ejemplo
 `var nombre = persona.nombre;`

### Desestructuracion 
Las últimas versiones de JavaScript nos permiten desglosar el objeto para acceder únicamente al atributo que nos interesa. Esto se consigue encerrando el nombre del atributo entre llaves { }.
Para no duplicar las variables se introduce el nombre de la variable como parámetro de la segunda variable.
Ejemplos: En los proximos ejemplo las dos lineas de codigo son completamente analogas

Ejemplo_1:
``` [javascript]
var nombre = persona.nombre;
var{ nombre } = persona;
```
Ejemplo_2:
``` [javascript]
let alias = seccion.alumno.nombre;
let {
  section: {
    nombre: alias
    } 
  } = section
```

***IMPORTANTE***
    Javascript se comporta de manera distinta cuando le pasamos un objeto como parámetro.

Cuando le pasamos un objeto a una funcion, este se pasan como una referencia del objeto, lo que significa que el objeto es modificado incluso fuera de la funciona.
Para solucionar esto se puede crear un objeto diferente o auxiliar. Esto lo podemos hacer colocando tres puntos antes del nombre del objeto(lo cual crea un desgloce del objeto).
Ejemplo:

```
aux = {
       …persona,
    }
```

# Librerias Standar de Js

## Timer
Los timer nos permiten ejecutar funciones despues de determinado tiempo. En js existen 2:

1. setInterval(function, x) : Ejecuta una "function" cada "x" intervalo de milisegundos 

2. setTimeout(functino ,x) : Ejecuta una "function" en "x" milisegundos

# Comparaciones

Existen varias maneras de comparar variables u objetos dentro de javascript.

Imaginemos que le asignamos a una variable *X* un valor numérico y a una variable *Y* un string. Para poder compararlos debemos agregar dos signos de igual (==). Esto los convierte al mismo tipo de valor y permite que se puedan comparar.

**NOTA:** Cuando realizamos operaciones es recomendable usar tres símbolos de igual (===). Esto permite que JavasScript no iguale las variables que son de distinto tipo. Es recomendado que se use el triple igual siempre que se estén comparando variables.

Recuerda existen cinco tipos de datos que son primitivos:

1. Boolean
2. Null
3. Undefined
4. Number
5. String

***MUY IMPORTANTE:*** Cuando comparamos objetos en Js, lo que hacemos es preguntar por la *referenacia en memoria RAM a la(s) variable(s)* que estamos consultando.

# Funciones
Son fracciones de código reutilizable.

- Para definir una función utilizaremos la palabra reservada  *function*.
- Delimitamos el cuerpo de la función usando llaves { }.
- Los parámetros de la función son variables que se pasan a la función escribíendolos entre paréntesis ().

Ejemplo:

``` [javascript]
function nameFunction (var1, var2, ...,varn){
    code...
}
```
**Nota:** JavaScript es un lenguaje interpretado, esto quiere decir que intentará ejecutar el código sin importar si los parámetros que le pasemos a la función estén invertidos o incluso incompletos.

## Arrow Function

Las Arrow Functions permiten una nomenclatura más corta para escribir expresiones de funciones. Este tipo de funciones deben definirse antes de ser utilizadas.

Al escribir las Arrow Functions no es necesario escribir la palabra function, y en algunos casos tampoco la palabra return, ni las llaves. Ejemplo:

``` [javascript]
const nameFunction = ( parameters ) => {
    code to executed ...
    return ...
}

const nameFunction = parameter => This is the value return
```

# Scope/ALcance
El Scope o ámbito es lo que define el tiempo de vida de una variable, en que partes de nuestro código pueden ser usadas.


Existen diferentes Scopes:
1. **Global Scope**
Variables disponibles de forma global se usa la palabra **var**, son accesibles por todos los scripts que se cargan en la página. Toda variable que está definida fuera del cuerpo de una funcion, bloque o modulo es una variable **global**.
**IMPORTANTE:**Aquí hay mucho riesgo de sobreescritura. No deben utilizarse

Ejemplo:
``` [JavaScript]
function printNumbers() {
  for (var i = 0; i < 10; i++) {
    setTimeout( () => console.log(i) , 100 )
  }
}
```

En el ejemplo anterio se utilizo *var* para definir la variable. Esto la convierte en una variable global. Llevandonos a un **ERROR** en lo que se desea que haga el codigo. Por este tipo de razones deben tratarse las variables globales con suma precaucion.

2. **Function Scope**
Variables declaradas dentro de una función, sólo visibles dentro de ella misma (incluyendo los argumentos que se pasan a la función).

Ejemplo1:
``` [JavaScript]
function printNumbers() {
  for (var i = 0; i < 10; i++) {
    const eventuallyPrintNumber = (n) => setTimeout( () => console.log(n) , 100 )
    eventuallyPrintNumber(i)
  }
}
```
El ejemplo anterior es un codigo correcto que hace lo que queremos, ya que al manejar la *variable* como un *parametro* esta pertenece al scope local de la funcion. recordando sus valores en cada iteracion.

3. **Block Scope**
Variables definidas dentro de un bloque, por ejemplo variables declaradas dentro un loop while o for. Se usa *let* y *const* para declarar este tipo de variables.

``` [JavaScript]
function printNumbers() {
  for (let i = 0; i < 10; i++) {
    setTimeout( () => console.log(i) , 100 )
  }
}
```
El codigo anterior hace exactamente lo que queremos que haga, con tan solo hacer el cambio de *var* a *let*, el codigo funciona a la perfeccion, ya que las variables declaradas con **let** y **const** trabajan sobre un bloque de ambito  local. Por lo que para cada iteracion el bloque recordara cual es la variable asignada para el.


4. **Module Scope**
Cuando se denota un **script** de tipo **module** con el atributo **type="module** las variables son limitadas al archivo en el que están declaradas. La forma de acceder a ellas desde otro ambito es por medio de la importacion del modulo.

Ejemplo:

Archivo1:  media-player.js
``` [JavaScript]
  import MediaPlayer from './MediaPlayer.js';

  const video = document.querySelector('video');
  const player = new MediaPlayer({ el: video });

  const button = document.querySelector('button');
  button.onclick = () => player.togglePlay();
```

Archivo2: index.js
``` [JavaScript]
function MediaPlayer(config) {
  this.media = config.el;
}

MediaPlayer.prototype.play = function() {
  this.media.play();
};

MediaPlayer.prototype.pause = function() {
  this.media.pause();
};

MediaPlayer.prototype.togglePlay = function() {
  if (this.media.paused) {
    this.play();
  } else {
    this.pause();
  }
};

export default MediaPlayer;
```

Archivo3: index.js 
``` [HTML]
<html>
  <head>
    <title>PlatziMediaPlayer.js</title>
    <link
      rel="stylesheet"
      href="https://necolas.github.io/normalize.css/8.0.1/normalize.css"
    />
    <link rel="stylesheet" href="./assets/index.css" />
  </head>

  <body>
    <header>
      <h1>PlatziMediaPlayer.js</h1>
      <p>An extensible media player.</p>
    </header>

    <main class="container">
      <video class="movie">
        <source src="./assets/BigBuckBunny.mp4" />
      </video>

      <button>Play/Pause</button>
    </main>

    <script src ="index.js"></script>
  </body>
</html>
```

# Estructuras de Control

## Condicionales
Los condicionales nos permiten decidir si un código se ejecuta o no. Mediante un condicional (if) decidiremos si se ejecuta una parte de nuestro código cuando se cumpla o no cierta condición. Ejemplo

``` [javascript]
if (condition) {
    This code be executed if condition is true...
} else {
    This code be executed if confition is false...
}
```

## Bucles
Se utilizan para repetir una o más instrucciones un determinado número de veces o mientras/hasta que se cumpla una condicion.

### For
El bucle for, se utiliza para repetir una o más instrucciones un determinado número de veces.

Para escribir un bucle for se coloca la palabra for seguida de paréntesis y llaves.
Ej. for( ){ }. Dentro de los paréntesis irán las condiciones para ejecutar el bucle, y dentro las llaves irán las instrucciones que se deben repetir.
Ejemplo:
```
for (var i=0; i <N; i++) {
    code...
}
```

### While
While se ejecuta únicamente mientras la condición que se está evaluando es verdadera.

Ejemplo
``` [javascript]
while (condition) {
    code...
}
```

### Do...While
A diferencia de la instrucción while, un bucle do…while se ejecuta una vez antes de que se evalúe la expresión condicional.

Ejemplo
``` [javascript]
Do {
    code...
} while (condition)
```

## Switch
Switch se utiliza para realizar diferentes acciones basadas en múltiples condiciones.

Break, sirve para que el browser se salte un bucle.

``` [javascript]
switch (variable) {
    case value1:
        code...
        break;
    case value2:
        code...
        break;
    case valueN:
        code...
        break;
    default:
        code...
        break;
}
```

# Arrays
Los arrays son estructuras que nos permiten organizar elementos dentro de una collección. Estos elementos pueden ser números, strings, booleanos, objetos, etc.

## Declaracion

```
var nombres = ['juan','pedro','jesus','mario'];
```
## Metodos

### filter
Para filtrar siempre necesitamos establecer una condición.

El método filter ( ) crea una nueva matriz con todos los elementos que pasan la prueba implementada por la función proporcionada.

Recuerda que si no hay elementos que pasen la prueba, filter devuelve un array vacío.
Ejemplo:
```
newArray = array.filter(function (parameter) {
    filtering logic
    return boolean
})
```

### map
El método map() itera sobre los elementos de un array en el orden de inserción y devuelve un array nuevo con los elementos modificados.

```
newArray = array.map(function (parameters) {
    maping logic
})
```
### reduce
El método reduce() nos permite reducir, mediante una función que se aplica a cada uno de los elemento del array, todos los elementos de dicho array, a un valor único.

# Closure
Un closure, básicamente, es una función que recuerda el estado de las variables al momento de ser invocada, y conserva este estado a través de reiteradas ejecuciones.

Estas nos sirven principalmente para tres cosas:
1. **IIFE**(Immediately invoked function expression)
Son funciones que se ejecutan tan pronto como se definen. Es un patrón de diseño también conocido cómo **función autoejecutable** (Self-Executing Anonymous Function  ) y se compone por dos partes.
- La primera es la función anónima con alcance léxico encerrado por el  `Operador de Agrupación ()`. Esto impide accesar variables fuera del IIFE, así cómo contaminar el alcance (scope) global. 

- La segunda parte crea la expresión de función cuya ejecución es inmediata (), siendo interpretado directamente en el engine de JavaScript.

Ejemplo:
``` [JavaScript]
 (function() {
  let color = 'green';
  function printColor() {
    console.log(color);
  }
```

2. **Retornar funciones**
Un aspecto *fundamental* de los **closures** es que son funciones que retornan otras funciones.
Ejemplo:
```[javaScript]
function crearSaludo(finalDeFrase) {
  return function (nombre) {
    console.log(`Hola ${nombre} ${finalDeFrase}`)
  }
}

const saludoArgentino = crearSaludo('che')
const saludoMexicano = crearSaludo('güey')
const saludoColombiano = crearSaludo('amigo')

saludoArgentino('Sacha') // Hola Sacha che
saludoMexicano('Sacha') // Hola Sacha güey
saludoColombiano('Sacha') // Hola Sacha amigo
```

3. **Variables privadas**
Los **closures** nos sirven para tener algo *parecido* a variables privadas, característica que no tiene JavaScript por default. Es decir encapsulan variables que no pueden ser modificadas directamente por otros objetos, sólo por funciones pertenecientes al mismo.
Ejemplo:
``` [JavaScript]
function makeCounter(n) {
  let count = n;

  return {
    increase: function() {
      count = count + 1;
    },
    decrease: function() {
      count = count - 1;
    },
    getCount: function() {
      return count;
    },
  };
}

let counter = makeCounter(7);
```
En el ejemplo anterior tenemos una objeto(recuerda que en Js las variables son objetos realmente). con un atributo interno privado.

# Prototipos (Clases)
En Javascript todo son objetos, no tenemos clases, no tenemos ese plano para crear objetos.

Todos los objetos “heredan” de un prototipo que a su vez hereda de otro prototipo y así sucesivamente creando lo que se llama la **prototype chain**.

La *keyword* **new** crea un nuevo objeto que “hereda” todas las propiedades del prototype de otro objeto. No confundir prototype con **proto** que es sólo una propiedad en cada instancía que apunta al prototipo del que hereda.

## Bases del leguaje
Lo que se describe a continuacion es parte de las bases del lenguaje, dicha sintaxis ya no es muy utilizada, mas sin embargo es importante tener dichos conceptos claros.

Las clases(aunque en Js hablamos mas de "prototipos" y no mucho de "clases") son funciones cuya sintaxis tiene dos componentes:
- expresiones
- declaraciones

**Definicion**

Para definir un prototipo solo debemos definir una funcion. Ejemplo

``` [javascript]
function prototypeName (parameters) {
    // this is code of builder
    this.attribute1 = value1
    this.attribute2 = value2
}

// this is a method of the prototype
prototypeName.prototype.methodName = function (parameters) {
    code..
}

var obj = new prototypeName(parameters)
```

## A partir de ECMAScript2015
A partir del 2015 las actualizaciones en el lenguaje trajeron consigo la palabra clave "class" y una forma mas sencilla de definir prototipos y de hacer "herencia" entre estos prototipo.

**Importante:** Se debe tener en cuenta que Js no cuenta con *clases* ni con el *keyword new*. Estos son una "azucar sintactica", pero en el fondo el lenguaje sigue trabajando con prototipos.

``` [javascript]
class prototypeName extends prototypePather {
    constructor (parameters){        
        super(parametersPather);
        this.attribute1 = value1;
        this.attribute2 = value2;
    }
}

// this is a method of the prototype
methodName (parameters) {
    code..
}

var obj = new prototypeName(parameters)
```
## Obtener prototipo
La forma correcta de obterner y manejar el *prototype* de un *objeto* es atraves de `Object.getPrototyptOf(objeto)`

## Herencia Prototipal
Por default los objetos en JavaScript tienen cómo prototipo a **Object** que es el punto de partida de todos los objetos, es el prototipo padre. Object es la raíz de todo, por lo tanto tiene un prototipo padre undefined.

Cuando se llama a una función o variable que no se encuentra en el mismo objeto que la llamó, se busca en toda la prototype chain hasta encontrarla o regresar undefined.

La función **hasOwnProperty** sirve para verificar si una propiedad es parte del objeto o si viene heredada desde su prototype chain.

# This
*This* se refiere a un objeto, ese objeto es el que actualmente está ejecutando un pedazo de código.

No se puede asignar un valor a this directamente y este depende de en que scope nos encontramos:

- Cuando llamamos a this en el **Global Scope** o **Function Scope**, se hace referencia al objeto *window*. A excepción de - cuando estamos en *strict mode* que nos regresará undefined.
- Cuando llamamos a this desde **una función** que está contenida en un objeto, this se hace referencia a *ese objeto*.
- Cuando llamamos a this desde una **“clase”**, se hace referencia a la *instancia generada* por el *constructor*.

## Métodos call, apply y bind
Estas funciones nos sirven para establecer el valor de this, es decir cambiar el contexto que se va usar cuando la función sea llamada.

Las funciones **call**, **apply** y **bind** son parte del prototipo Function. Toda función usa este prototipo y por lo tanto tiene estas tres funciones.

- **functionName.call()**
Ejecuta la función recibiendo como primer argumento el this y los siguientes son los argumentos que recibe la función que llamó a call.
Ejemplo:
``` [JavaScritp]
  // Establece `this` usando `call`
  function saludar() {
    console.log(`Hola. Soy ${this.name} ${this.apellido}`);
  }

  const richard = {
    name: 'Richard',
    apellido: 'Kaufman López',
  };

  saludar.call(richard);

  // Establece `this` usando `call` y pasar argumentos a la función
  function caminar(metros, direccion) {
    console.log(`${this.name} camina ${metros} metros hacia ${direccion}.`);
  }

  caminar.call(richard, 400, 'norte');

```
- **functionName.apply()**
Ejecuta la función recibiendo como primer argumento el this y como segundo un arreglo con los argumentos que recibe la función que llamó a apply.
Ejemplo:
``` [JavaScript]
  function caminar(metros, direccion) {
    console.log(`${this.name} camina ${metros} metros hacia ${direccion}.`);
  }

  const richard = {
    name: 'Richard',
    apellido: 'Kaufman López',
  };

  // Establece `this` usando `apply` y pasar argumentos a la función
  const valores = [800, 'noreste'];
  caminar.apply(richard, valores);
```

- **functionName.bind()**
Recibe como primer y único argumento el this. **No ejecuta la función**, sólo regresa otra función con el nuevo this integrado.
``` [JavaScript]
  function saludar() {
    console.log(`Hola. Soy ${this.name} ${this.apellido}`);
  }

  const richard = {
    name: 'Richard',
    apellido: 'Kaufman López',
  };

  saludar.call(richard);

  // Establecer `this` en una nueva función usando `bind`
  
  const daniel = { name: 'Daniel', apellido: 'Sánchez' };
  const danielSaluda = saludar.bind(daniel);
  danielSaluda();

  const danielCamina = caminar.bind(daniel, 2000);
  danielCamina('oeste');

```

# Getters y setters
Los getters y setters son funciones que podemos usar en un objeto para tener propiedades virtuales. Se usan los keywords set y get para crear estas propiedades.

Estas propiedades al ser funciones pueden llevar una validación de por medio y ser usadas con el operador de asignación como si fueran una variable más dentro del objeto.
Tambien nos sirve para tener control sobre lo que  exponemos del objeto al Scope ya que no requerimos del keywork "this" para editar algun atributo.
Ejemplo: 
``` [JavaScript]
let persona = {
  nombre: 'Yeison',
  apellido: 'Daza',
  get nombreCompleto() {
    return`${nombre} ${apellido}`
  },
  set nombreCompleto(nom) {
    const palabras = nom.split(' ');
    this.nombre = palabras[0] || '';
    this.apellido = palabras[1] || '';
  }
}

persona.nombreCompleto = 'Camilo Sanchez'

console.log(persona.nombre); //camilo
console.log(persona.apellido); //sanchez
```

# Proxy
El objeto **[Proxy](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Proxy)** se usa para definir un comportamiento personalizado para operaciones fundamentales (por ejemplo, para observar propiedades, cuando se asignan, enumeración, invocación de funciones, etc).
Sirve para interceptar la lectura de propiedades de un objeto (los get, y set) entre muchas otras funciones. Así, antes de que la llamada llegue al objeto podemos manipularla con una lógica que nosotros definamos. Esto lo hacemos por medio de "trampas"".
Ejemplo:
En este simple ejemplo el número **37** se devuelve como valor predeterminado cuando la propiedad `name` no se encuentra en el objeto. Se utilizando el manejador `get`.
``` [JavaScript]
var handler = {
    get: function(target, name){
        return name in target?
            target[name] :
            37;
    }
};

var p = new Proxy({}, handler);
p.a = 1;
p.b = undefined;

console.log(p.a, p.b); // 1, undefined
console.log('c' in p, p.c); // false, 37
```

# Asincronismo
JavaScript sólo puede hacer una cosa a la vez, sin embargo; es capaz de delegar la ejecución de ciertas funciones a otros procesos. Este modelo de concurrencia se llama EventLoop.

JavaScript delega en el navegador ciertas tareas y les asocia funciones que deberán ser ejecutadas al estas tareas ser completadas. Estas funciones se llaman *callbacks*, y una vez que el navegador ha "regresado" con la respuesta(de las tareas), el callback asociado pasa a una cola de tareas para ser ejecutado una vez que JavaScript haya terminado todas las instrucciones que están en la pila de ejecución.

**IMPORTANTE**
    Si se acumulan funciones en la cola de tareas y JavaScript se encuentra ejecutando procesos muy pesados, el EventLoop quedará *bloqueado* y esas funciones pudieran tardar demasiado en ejecutarse.

En principio, cualquier tarea que se haya delegado al navegador a través de un *callback*, deberá esperar hasta que todas las instrucciones del programa principal se hayan ejecutado. Por esta razón el tiempo de espera definido en funciones como *setTimeout*, no garantizan que el callback se ejecute en ese tiempo exactamente, sino en cualquier momento a partir de allí, sólo cuando la cola de tareas se haya vaciado.

## Callback
Un callback es una función que se pasa a otra función como un argumento. Esta función se invoca, después, dentro de la función externa para completar alguna acción.

## Orden en el asincronismo
Una manera de asegurar que se respete la secuencia en que hemos realizado múltiples tareas es utilizando *callbacks*, con lo que se ejecutará luego, en cada llamada. Lo importante es que el llamado al callback se haga a través de una función anónima. Sin embargo, al hacerlo de esta manera generamos una situación poco deseada llamada CallbackHell. Ejemplo:

``` [javaScript]
const API_URL = "https://swapi.co/api/";
const PEOPLE_URL = "people/:id";
const opts = { crossDomain: true };

function obtener_personaje(id, callback) {
	consturl = `${API_URL}${PEOPLE_URL.replace(":id", id)}`;
	$.get(url, opts, function(persona) {
		console.log(`Hola yo soy ${persona.name}`);
		if (callback) {
			callback();
		}
	});
}

obtener_personaje(1, function() {
	obtener_personaje(2, function() {
		obtener_personaje(3, function() {
			obtener_personaje(4, function() {
				obtener_personaje(5, function() {
					obtener_personaje(6);
				});
			});
		});
	});
});
```

## Promesas
Son justamente eso, promesas de valores que aun no conocemos, pero prometemos conocer en un futuro. Las promesas tienen tres estados:

- pending
- fullfilled
- rejected

Las promesas se invocan de la siguiente forma:

``` javascript
Promesa = new Promise( ( resolve, reject ) => {
  // --- llamado asíncrono
  if( todoOK ) {
     // -- se ejecutó el llamado exitosamente
     resolve(parm_okey_1, parm_okey_2)
  } else {
     // -- hubo un error en el llamado
     reject(parm_fail_1, parm_okey_1)
  }
} )

Promesa
  .then(function(parm_okey_1, parm_okey_2) {
    // este codigo se ejecuta cuando "resolve()" es llamado
  })
  .catch(function(parm_okey_1, parm_okey_1) {
    // este codigo se ejecuta cuando "reject()" es llamado
  })

```
### En Serie
A diferencia de los callbacks en el CallbackHell, que terminan estando anidados unos dentro de otros, cuando se usan Promesas la ejecución de las llamadas no se hacen de manera anidada sino de manera encadenada, al mismo nivel una debajo de la otra, lo que hace que el código sea mucho más legible y mantenible.

Ejemplo(replica del codigo anterior con los *callback*):

``` javaScript
const API_URL = "https://swapi.co/api/";
const PEOPLE_URL = "people/:id";
const opts = { crossDomain: true };

function obtener_personaje(id) {
	return new Promise((resolve, reject) => {
		const url = `${API_URL}${PEOPLE_URL.replace(":id", id)}`;
		$.get(url, opts, function(data) {
			resolve(data);
		}).fail(() => reject(id));
	});
}

function on_error(id) {
    console.log(`Sucedio un error al obtener el personaje ${id}`)
}


obtener_personaje(1)
    .then(personaje => {console.log(`El personaje 1 es ${personaje.name}`)
    return obtener_personaje(2)
    })
    .then(personaje => {console.log(`El personaje 2 es ${personaje.name}`)
    return obtener_personaje(3)
    })
    .then(personaje => {console.log(`El personaje 3 es ${personaje.name}`)
    return obtener_personaje(4)
    })
    .then(personaje => {console.log(`El personaje 4 es ${personaje.name}`)
    return obtener_personaje(5)
    })
    .then(personaje => {console.log(`El personaje 5 es ${personaje.name}`)
    return obtener_personaje(6)
    })
    .then(personaje => {console.log(`El personaje 6 es ${personaje.name}`)
    })
    .catch(on_error)
```

### En paralelo
Para hacer el llamado a múltiples promesas, nos apoyamos en un array de ids con el que luego construimos otro arreglo de Promesas, que pasaremos como parámetro a Promise.all( arregloDePromesas ), con las promesas podemos encadenar llamadas en paralelo, algo que no es posible usando callbacks.
Ejemplo:
``` javascript
const API_URL = 'https://swapi.co/api/'
const PEOPLE_URL = 'people/:id'
const opts = { crossDomain: true }

function obtenerPersonaje(id) {
  return new Promise((resolve, reject) => {
    const url = `${API_URL}${PEOPLE_URL.replace(':id', id)}`
    $
      .get(url, opts, function (data) {
        resolve(data)
      })
      .fail(() => reject(id))
  })
}

function onError(id) {
  console.log(`Sucedió un error al obtener el personaje ${id}`)
}

var ids = [1, 2, 3, 4, 5, 6, 7]
var promesas = ids.map(id => obtenerPersonaje(id))
Promise
  .all(promesas)
  .then(personajes => console.log(personajes))
  .catch(onError)
```
### En carrera
Permite ejecutar multiples promesas al mismo tiempo y ejecutar aquella que termine primero ejemplo:

``` javascript
const getUserAll = new Promise(function(todoBien, todoMal) {
  // llamar a un api
  setTimeout(function() {
    // luego de 3 segundos
    todoBien('se acabó el tiempo');
  }, 5000)
})

const getUser = new Promise(function(todoBien, todoMal) {
  // llamar a un api
  setTimeout(function() {
    // luego de 3 segundos
    todoBien('se acabó el tiempo 3');
  }, 3000)
})

Promise.race([
  getUser,
  getUserAll,
])
.then(function(message) {
  console.log(message);
})
.catch(function(message) {
  console.log(message)
})

// En este ejemplo solo se ejecutara getUser
```

**NOTA:** Podemos manejar los errores de las promesas si en el then pasamos un segundo callback, este segundo callback maneraja el error de esa promesa.

## Async-await
Es la manera más simple y clara de realizar tareas asíncronas. Await detiene la ejecución del programa hasta que todas las promesas sean resueltas. Para poder utilizar esta forma, hay que colocar async antes de la definición de la función, y encerrar el llamado a Promises.all() dentro de un bloque try … catch.
Ejemplo:
``` javaScript
const API_URL = 'https://swapi.co/api/'
const PEOPLE_URL = 'people/:id'
const opts = { crossDomain: true }

function obtenerPersonaje(id) {
  return new Promise((resolve, reject) => {
    const url = `${API_URL}${PEOPLE_URL.replace(':id', id)}`
    $
      .get(url, opts, function (data) {
        resolve(data)
      })
      .fail(() => reject(id))
  })
}

function onError(id) {
  console.log(`Sucedió un error al obtener el personaje ${id}`)
}

async function obtenerPersonajes() {
  var ids = [1, 2, 3, 4, 5, 6, 7]
  var promesas = ids.map(id => obtenerPersonaje(id))
  try {
    var personajes = await Promise.all(promesas)
    console.log(personajes)
  } catch (id) {
    onError(id)
  }
}

obtenerPersonajes()
```

**NOTA:** Cualquier funcion async-await retorna una promesa, por lo tanto si requerimos un valor retornado por esta lo obtendremos atraves de un then().

**NOTA:** Todos los errores de la funcion podran ser manejados dentro del cath de la promesa(Leer la nota anterior).

# Memoizacion
La memoización es una técnica de programación que nos permite ahorrar cómputo o procesamiento en JavaScript, al ir almacenando el resultado invariable de una función para que no sea necesario volver a ejecutar todas las instrucciones de nuevo, cuando se vuelva a llamar con los mismos parámetros. Es similar a usar memoria cache.
Ejemplo:
``` javaScript
function factorial(n) {
  if (!this.cache) {
    this.cache = {}
  }

  debugger
  if (this.cache[n]) {
    return this.cache[n]
  }

  if (n === 1) {
    return 1
  }

  this.cache[n] = n * factorial(n - 1)
  debugger
  return this.cache[n]
}
```

# Ajax
Ajax recibe dos parámetros los cuales son la url de la API y un objeto donde pondrás la configuración que se usara para realizar la petición. En la configuración se añaden dos funciones para manejar cuando la petición se realizo correctamente y cuando falla. Esta es la forma como se realizaria con jQuery un ejemplo sencillo seria el siguiente:

``` [javaScript]

$.ajax('https://randomuser.me/api/ ', {
  method: 'GET',
  success: function(data) {
    console.log(data)
  },
  error: function(error) {
    console.log(error)
  }
})
```

Peeeeero en el mundo moderno *JavaScript* internamente cuenta con una función llamada **fetch** que también realiza peticiones a una API. Al igual que Ajax necesita dos parámetros, una url y una configuración, pero si solo le mandas la url fetch usará una configuración por defecto donde el método HTTP será GET.
**fetch** te regresa una promesa, esa promesa al resolverse te da los datos de respuesta y tiene un método llamado json que te regresa otra promesa con los datos en formato JSON.

Ejemplo:

``` [javaScript]

fetch('https://randomuser.me/api/')
  .then(function (response) {
    // console.log(response)
    return response.json()
  })
  .then(function (user) {
    console.log('user', user.results[0].name.first)
  })
  .catch(function() {
    console.log('algo falló')
  });
```

Con **fetch** tenemos algo llamado **AbortController** que nos permite enviar una señal a una petición en plena ejecución para detenerla.

Ejemplo: 

``` [JAvaScript]
loadButton.onclick = async function() {
  startLoading();

  controller = new AbortController();

  try {
    const response = await fetch(url, { signal: controller.signal });
    const blob = await response.blob();
    const imgUrl = URL.createObjectURL(blob);
    img.src = imgUrl;
  } catch (error) {
    console.log(error.message);
  }
}

stopButton.onclick = function() {
  controller.abort();
  stopLoading();
};

```
En el codigo anterior tenemos un objeto **controloador**, que contiene una propiedad **signal** que nos servira para **cancelar** la peticion del fetch en el momento que lo necesitemos.
Bastara con emitirle una señal al controlador con el metodo **abort**. Que en este caso es llamado a traves de un boton.
NOTA: El metodo *blob* del response, no da la respuesta en un binario.
# Manejo de Errores
Para el manejo de errores utilizamos el bloqu de codigo **try..catch**. Dentro de *try* va el vloque de codigo que se va a intentar correr, si sucede un error se ejecutara el bloque *catch*. Ejemplo:

``` [JavaScript]
try {
  code..
} catch (error)
  code.. // el atributo 'error' contiene la informacion sobre el error ocurrido.
```

# Interaccion el DOM
## Selectores
Un selector nos sirve para poder manipular un objeto del DOM, puedes buscar dicho objeto ya sea por su id, clase, atributo, etc.

Dentro de JavaScript existen distintas funciones para hacer selectores, entre ellas se encuentra:

- **getElementById('id')**: recibe como parámetro el id del objeto del DOM que estás buscando. Te regresa un solo objeto.
- **getElementsByTagNamed('tag')**: recibe como parámetro el tag que estas buscando y te regresa una colección html de los elementos que tengan ese tag.
- **getElementsByClassName('class')**: recibe como parámetro la clase y te regresa una colección html de los elementos que tengan esa clase.
- **querySelector**: va a buscar el primer elemento que coincida con el selector(como los de css['.', '#', img, label, etc]) que le pases como parámetro.
- **querySelectorAll**: va a buscar todos los elementos que coincidan con el selector que le pases como parámetro.

Ejemplo:

``` [JavaScript]
  const $modal = document.getElementById('modal');
  const $overlay = document.getElementById('overlay');
  const $hideModal = document.getElementById('hide-modal');

  const $modalTitle = $modal.querySelector('h1');
  const $modalImage = $modal.querySelector('img');
  const $modalDescription = $modal.querySelector('p');
```
## Creacion/Edicion del DOM

### Templates

Desde ECMAScript 6 contamos con una nueva característica llamada template literals que se representan con las comillas invertidas ``, el ejemplo anterior pasaría a verse de esta forma:
``` [JavaScript]
`<div class=”container”>
    <p id=${id}>Hola Mundo<p>
<div>`
```
La forma en la que utilizamos los template en Js es:
``` [JavaScript]
  function videoItemTemplate(movie) {
    return (
      `<div class="primaryPlaylistItem">
        <div class="primaryPlaylistItem-image">
          <img src="${movie.medium_cover_image}">
        </div>
        <h4 class="primaryPlaylistItem-title">
          ${movie.title}
        </h4>
      </div>`
    )
  }
```
#### Implementando el template

Para convertir nuestra plantilla de texto a un Document Object Model necesitamos crear dentro de memoria un documento HTML, esto es posible gracias al método **document.implementation.createHTMLDocument** . A este documento HTML le vamos a añadir al body, mediante **innerHTML**, nuestra plantilla de texto. 
Este flujo es la magia que hay detrás de varias librerías y frameworks que nos ayudan a crear interfaces.

Ejemplo:

``` [JavaScript]
  function createTemplate(HTMLString) {
    const html = document.implementation.createHTMLDocument();
    html.body.innerHTML = HTMLString;
    return html.body.children[0];
  }
  function renderMovieList(list, $container) {
    $container.children[0].remove();
    list.forEach((movie) => {
      const HTMLString = videoItemTemplate(movie);
      const movieElement = createTemplate(HTMLString);
      $container.append(movieElement);
    })
  }
```
### Creacion de elementos HTML individuales
Vamos a crear un elemento HTML sin usar un template string. Para crear el elemento desde cero vamos a usar el método **document.createElement**, este recibe como parámetro la etiqueta html del elemento que se quiere crear.
*NOTA:* no funciona mandándole el template string.

Para añadirle un atributo al elemento que acabamos de crear haremos uso del método **setAttribute**. Este recibe dos parámetros, uno indicando el nombre del atributo que vamos a añadir y el segundo parámetro indicando el valor de dicho atributo.
Para añadir multiples atributos vamos a crear una función.

Ejemplo:

``` [javaScript]
  function setAttributes($element, attributes) {
    for (const attribute in attributes) {
      $element.setAttribute(attribute, attributes[attribute]);
    }
  }

    const $loader = document.createElement('img');
    setAttributes($loader, {
      src: 'src/images/loader.gif',
      height: 50,
      width: 50,
    })

```

## Eventos 
### Escuchar Evento
Para que un elemento HTML pueda escuchar algún evento debemos usar el método **addEventListener**. Este método recibe dos parámetros, el nombre del evento que va a escuchar y la función que se va a ejecutar al momento de que se accione el evento.
Ejemplo:
```[JavaScript]
  const $form = document.getElementById('form');

  $form.addEventListener('submit', (event) => {
    event.preventDefault();
  })
```
*NOTA:* La página se recarga al momento de ejecutarse el evento submit, para evitar esto debemos quitarle la acción por defecto que viene en submit usando el método event.preventDefault().

*NOTA:* Se puede consultar los eventos disponibles para los elenmentos HTML desde [aqui](https://developer.mozilla.org/es/docs/Web/API/Event)

## Formulario
Algo muy comun en el desarrollo de aplicaciones en especial las CRUD es la intercacion con formularios para esto Js nos ofrece el metodo **FormData** el cual recibe como parametro un elemento HTML form para interactuar con sus datos.
Sus principales metodos son **get('name')** y **set('name', 'value')** donde 'name' es el nombre del sub-elemento del formulario. Ejemplo:

``` [Java Script]
$form = document.getElementById('form_1');
$serch = document.getElementById('buscador_peli');


Data = new FormData($form);
Data = set('buscador_peli','La momia');
Data = get('buscador_peli'); // La momia

$serch.dataset.atributte; // Valor de 'atribute'
```

## IntersectionObserver
Sirve para observar elementos y ver cual es su posicion. En el caso de que cruzen un umbral que nosotros definimos nos lo va a notificar para tomar acción.

El umbral se define por el porcentaje que tiene intersección con el viewport, con la parte visible de nuestra página.

IntersectionObserver recibe dos parametros:
- Handle : Sera la funcion que se ejecute al momento de que el observador nos notifiique.
- config : Es un JSON que contiene las configuraciones del observador(threshold es una de ellas y la que nos dice en que pocentaje de interseccion nos notificara)

Ejemplo:
``` [JavaScript]
class AutoPause {
  constructor() {
    this.threshold = 0.25;
    this.handleIntersection = this.handleIntersection.bind(this);
  }

  run(player) {
    this.player = player;

    const observer = new IntersectionObserver(this.handleIntersection, {
      threshold: this.threshold,
    });

    observer.observe(this.player.media);
  }

  handleIntersection(entries) {
    const entry = entries[0];

    const isVisible = entry.intersectionRatio >= this.threshold;

    if (isVisible) {
      this.player.play();
    } else {
      this.player.pause();
    }
  }
}

export default AutoPause;
```

## VisibilityChange
El **visibilityChange** es un evento y forma parte del API del DOM llamado **Page Visibility** y nos deja saber si el elemento es visible, pude ser usado para ejecutar una acción cuando cambiamos de pestaña. Así podemos ahorrar batería y mejorar la UX.

# Service Workers
Sirven para hacer que nuestras aplicaciones funcionen Offline. 

Muy usados en las **Progressive Web Apps **(PWA) los ServiceWorkers son una capa que vive entre el navegador y el Internet.

Parecido a como lo hacen los proxys van a interceptar peticiones para guardar el resultado en cache y la próxima vez que se haga la petición tomar del cache ese resultado.

Los Service workers se instalan en el navegador, aunque no funcionan como una APP

Ejemplo de un Service Workers
sw.js :
``` [JavaScript]
const VERSION = 'v1';

self.addEventListener('install', event => {
  event.waitUntil(precache());
});

self.addEventListener('fetch', event => {
  const request = event.request;
  // get
  if (request.method !== 'GET') {
    return;
  }

  // buscar en cache
  event.respondWith(cachedResponse(request));

  // actualizar el cache
  event.waitUntil(updateCache(request));
});

async function precache() {
  const cache = await caches.open(VERSION);
  return cache.addAll([
    '/',
    '/index.html',
    '/assets/index.js',
    '/assets/MediaPlayer.js',
    '/assets/plugins/AutoPlay.js',
    '/assets/plugins/AutoPause.js',
    '/assets/index.css',
    '/assets/BigBuckBunny.mp4',
  ]);
}

async function cachedResponse(request) {
  const cache = await caches.open(VERSION);
  const response = await cache.match(request);
  return response || fetch(request);
}

async function updateCache(request) {
  const cache = await caches.open(VERSION);
  const response = await fetch(request);
  return cache.put(request, response);
}
```

**IMPORTANTE:** Es una caracteristica nueva por lo que no esta disponible aun en todoos los navegadores.
**IMPORTANTE2:** Cuando estemos trabajando en desarrollo debemos habilitar la opcion "Update on reload" en la seccion de *Application > Service Workeers* que se encuentra en los Dev Tools
# localStorage y sessionStorage
**sessionStorage** mantiene un área de almacenamiento separada para cada origen que está disponible mientras dure la sesión de la página (mientras el navegador esté abierto, incluyendo recargas de página y restablecimientos).
**localStorage** hace lo mismo, pero persiste incluso cuando el navegador se cierre y se reabra.

Estos estan disponibles están disponibles mediante las propiedades *Window.sessionStorage* y  *Window.localStorage*

Estos mismos tiene los metodos *clear*, *setItem*  y *getItem* para elimirar, configurar y obtener sus valores respectivamente.

***IMPORTANTE:*** Estos metodos solo permiten el almacenamiento de **texto plano**. Si deseamos almacenar objetos podemos utilizar el metodo *JSON.stringify({objec})* para hacer la transformacion. Para volder un texto plata un objeto utilizamos la funcion *JSON.paser('{"name":value}')*.

# Generadores
Los generadores son funciones especiales, pueden **pausar** su ejecución y luego **volver** al punto donde se quedaron recordando su scope.

Algunas de sus características:

- Los generadores regresan una función.
- Empiezan suspendidos y se tiene que llamar **next** para que ejecuten.
- Regresan un *value* y un *boolean* **done** que define si ya terminaron.
- **yield** es la instrucción que regresa un valor cada vez que llamamos a **next** y detiene la ejecución del generador.

Los generadores se definen creando unas funcion seguida de un **\***. Ejemplo:
``` [JavaScript]
//Generator Basico
function* simpleGenerator() {
  console.log('GENERATOR START');
  yield 1;
  yield 2;
  yield 3;
  console.log('GENERATOR END');
}

// Podemos hacer generadores infinitos.
function* idMaker() {
  let id = 1;
  while (true) {
    yield id;
    id = id + 1;
  }
}

// Cuando llamamos next también podemos pasar valores que la función recibe.
function* idMakerWithReset() {
  let id = 1;
  let reset;
  while (true) {
    reset = yield id;
    if (reset) {
      id = 1;
    } else {
      id = id + 1;
    }
  }
}

// Ahora hagamos un ejemplo un poco más complejo: la secuencia fibonacci
function* fibonacci() {
  let a = 1;
  let b = 1;
  while (true) {
    const nextNumber = a + b;
    a = b;
    b = nextNumber;
    yield nextNumber;
  }
}

```

# ¿Como funciona JavaScript?

## Parsers y el Abstract Syntax Tree
El JS Engine recibe el código fuente y lo procesa de la siguiente manera:

- El **parser** descompone y [crea tokens](https://esprima.org/demo/parse.html) que integran el **[AST](https://astexplorer.net)**(Abstract syntax tree).
- Se compila a **bytecode** y se ejecuta.
- Lo que se pueda se **optimiza a machine code** y se reemplaza el código base.

Un **SyntaxError** es lanzado cuando el motor JavaScript encuentra partes que no forman parte de la sintaxis del lenguaje y esto lo logra gracias a que se tiene un **AST** generado por el parser.

El *parser* es del 15% al 20% del proceso de ejecución y es triste, pero la **mayoria** del JavaScript en una paga nunca se ejecuta.
Por lo que *parsear* el código justo en el momento que lo necesitamos y no antes de saber si se va a usar o no es super importante. Esto lo podemos hacer por medio de **bundling** y **code splitting**.

### Creacion de una regla para AST
Vamos a usar el **AST** para crear una regla de **eslint**, este analizará estéticamente nuestro código a ver si hay que levantar un warning por violar la sintaxis. Muchas de estas reglas ya viene con e eslint, pero podemos agregar nuestras propias reglas. Vamos a usar la herramienta [AST Explorer](https://astexplorer.net/#/gist/16fc27fc420f705455f2b42b6c804aa1/42c2d7223f31edbb41bb9615f556d68cb7a793e4) para experimentar. Usaremos la configuración por defecto, veremos en la parte superior izquierda el código que vamos a ingresar, a la derecha el tree creado, en la parte inferior izquierda las funciones de las reglas(que crearemos) y a la derecha de eso la salida de nuestro código.

#### Test
En el **link** de **AST Explorer** ya tenemos un código escrito. Donde el la primera entrada tenemos las tareas que debe cumplir nuestro **fixer**.
``` [JavaScript]
const pi = 3.1415;
const half_pi = 1.57075;
// variable constantes
// variables que guarden un numero

// El nombre de la variable tiene que estar en UPPERCASE
```
A la derecha tenemos el árbol completo de todas estas declaraciones y gracias a el podemos manipular, detectar errores o interpretar lo que escribamos. Luego implementamos una función que recibe la declaración de la variable y accedemos a los datos que nos ofrece el AST para lograr cumplir con los requerimientos de nuestro solucionador.
``` [JavaScript]
export default function(context) {
  return {
    VariableDeclaration(node) {
        // tipo de variable const
          if (node.kind === "const") {
          const declaration = node.declarations[0];

          // asegurarnos que el valor es un numero
          if (typeof declaration.init.value === "number") {
            if (declaration.id.name !== declaration.id.name.toUpperCase()) {
              context.report({
                node: declaration.id,
                message: "El nombre de la constante debe estar en mayúsculas",
                fix: function(fixer) {
                  return fixer.replaceText(declaration.id, declaration.id.name.toUpperCase())
                }
              })
            }
          }
        }
    }
  };
};
```

## Funcionamiento de JavaScript Engine
Una vez tenemos el **AST** ahora hay que convertirlo a Bytecode.

**Bytecode** es como el código assembler pero en lugar de operar en el procesador opera en la máquina virtual **V8** del navegador.

**Machine code** es el más bajo nivel, es código binario que va directo al procesador.

**El profiler** se sitúa en medio del bytecode y el optimizador

Cada máquina virtual tiene sus particularidades, por ejemplo V8 tiene algo llamado **Hot Functions**.

Cuando una sentencia función es ejecutada muy frecuentemente, V8 la denomina como una hot function y hace una optimización que consiste en convertirla a machine code para no tener que interpretarla de nuevo y agilizar su ejecución.

Cada navegador tiene su implementación de JavaScript Engine:

SpiderMonkey - Firefox
Chackra - Edge
JavaScriptCore - Safari
V8 - Chrome
Carakan - Opera

## Event Loop
El **Event Loop** hace que Javascript parezca ser multihilo a pesar de que corre en un solo proceso.

Javascript se organiza usando dos principales estructuras de datos:

1. **Stack**: comienza vacio y va apilando de forma organizada las diferentes instrucciones que se llaman. Lleva así un rastro de dónde está el programa, en que punto de ejecución nos encontramos. Este apunta a aspectos como el Scope
2. **Memory Heap**: De forma desorganizada se guarda información de las variables y del scope.


Para explicar como se ejecutan los procesor asincronos o progrmados es necesario definir que es un Queue. Un Queue es una estructura  de datos muy parecida a un stack.
Los Queue utilizados por Js son:
1.  **Schedule Tasks.** Aquí se agregan a la cola, las tareas programadas para su ejecución.
2. **Task Queue**. Aquí se agregan las tareas que ya están listas para pasar al stack y ser ejecutadas. El stack debe estar vacío para que esto suceda.
3. **MicroTask Queue**. Aquí se agregan las promesas. **Esta Queue es la que tiene mayor prioridad**.

Todos estas estructuras de informacion trabajan de una forma fluida gracias al Event Loop.

El Event Loop es un loop que está ejecutando todo el tiempo y pasa periódicamente revisando las queues y el stack moviendo tareas entre estas dos estructuras.

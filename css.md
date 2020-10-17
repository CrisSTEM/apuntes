---
title: "CSS - Hojas de estilo en cascada"
slug: "css"
description: "👩‍🎨"
keywords: [programacion, desarrollo, software, css, frontend]
draft: false
tags: []
math: false
toc: false
---
# 1 Fundamentos

## 1.1 Sintaxis
Puede echarle un vistazo a al vocabulario de css [aqui](http://apps.workflower.fi/vocabs/css/en#comment)
- Comentarios:

`/* Esto es un comentario en CSS */`

## 1.2 Estilos del navegador
Por defecto cada browser contiene un estilo de css. Esto puede ocasionar distinta clase de problemas a la hora de nosotros implementar nuestros estilos.
La manera de resolver esto es utilizando una libreria de terceros llamada [normalize](https://necolas.github.io/normalize.css/) que como su nombre lo indica nos normaliza los estilos por defecto que vayamos a utilizar.

## 1.3 Soporte
En [esta pagina](https://caniuse.com) podemos buscar una caracteristica o propiedad y ver su soporte en los navegadores

## 1.4 Variables
Son espacios en memoria que almacenan un valor.
### 1.4.1 Declaracion
```css
/* Esta es la manera de declarar y redefinir las variables en css: */
:root {
    --nameVar1: value;
    --nameVar2: value;
}
```
### 1.4.2 Llamado
```css
body {
    --color: red;
    background-color: var(--color, blue);
}
/* El segundo valor pasado a la funcion 'var()' es un failback, por si el primer parametro falla. */
```
### 1.4.3 Scope
Tienen un scope de DOM. Tienen herencia y cacascada al igual que otras propiedades de CSS.

### 1.4.4 Acceso a variables CSS desde Js
1. La funcion **getComputedStyle(element)** nos **retorna un objeto** del elemento "element" una vez el navegador ya ha hecho todos los calculos respectivos para renderizar.

2. Para leer una propiedad ejecutamos el siguiente metodo al objeto del paso anterior: `getPropertyValue('propertyName')`. Donde "propertyName" es el nombre de la propiedad a buscar.

3. Para setear una variable: `element.style.setProperty('propertyName', 'Value')`.

# 2 Selectores
Se dividen esencialmente en 3 tipos:

1. Sencillos.
2. Compuestos.
3. De atributos.

## 2.1 Sencillos
Son selectores de un solo elemento. Existen varios:

### 2.1.1 Selector de elemento o tipo
Es el mas sencillo de todos que es basicamente el nombre de una etiqueta HTML o XML. Ejemplo:

`body { ... }`

*NOTA:* **NO** es recomendado modificar estos estilos a menos que estes muy claro de lo que estas haciendo.

### 2.1.2 Selectores de clases
Son los mas recomentados y utiles al momento de escribir los estilos de un proyecto. Se escribe anteponiendo el nombre de la clases por un punto(.). Ejemplo:

`.nameClass { ... }`

### 2.1.3 Selectores de ID
Se escribe anteponiendo el nombre de la clases por un  hash(#). Ejemplo:

`#nameID { ... }`

*NOTA:* Su uso no es para nada recomendado en css

### 2.1.4 Selector universal
Se denota con el caracter *. Como su nombre lo indica le aplica los estilos a todos los elementos. Ejemplo:

`* { ... }`

**IMPORTANTE:** *NO* utilices este selector a menos que estes muy claro(pero extremadamente claro) de lo que estas haciendo y tienes ya tienes un nivel elevado en CSS. **Puede ocasionar bugs**.

## 2.2 Compuestos
Estos a su vez se dividen en varios tipos. Es importante aclarar que el nombre oficial no es 'selectores compuestos' este nombre es unicamente para objetivos didacticos.

### 2.2.1 Selectores agrupados
Nos permiten asignar estilos a varios selectores en un mismo bloque de codigo. Esto lo hacemos separando los selectores con comas(,). Ejemplo:
```CSS
/* El siguiete codigo coloca un fondo color rojo para los elementos de las clase
'nameClass1', el elemento de ID 'nameID' y los parrafos. */

.nameClass1,
#nameID,
p {
    background: red;
}
```

### 2.2.2 Selectores desendientes
Nos permiten asignar estilos a un elemento que sea *desendiente* (hijo, nieto, etc) de otro elemento. Esto lo hacemos dejando un escio en blanco(' ') entre los selectores. Ejemplo:

```css
/* El siguiente codgio le coloca un fondo blanco a los parrafos que sean hijo de la clase dashboard-dark*/

.dashboard-dark p {
    background: white;
}
```

**IMPORTANTE:** esta debe ser una de las *ULTIMAS* opciones que utilicemos. Esto nos puede traer o ocasionar bugs.

*NOTA:* Debes tener cuidado de dejar el espacio en blanco entre los selectores, de no ser asi estas indicando que quieres seleccionar un elemento que cumple con TODAS las caracteristicas descritas(para el caso del ejemplo anterior, un parrafo que pertenece a la clase dashboard-dark).

### 2.2.3 Selector hijo directo
Es utilizador para asignar estilo a un *hijo directo*(no nietos, ni hermanos, ni nada mas. Solo hijos directos) de otro elemento. Esto lo hacemos a traves del operador *mayor que(>)* Ejemplo:
```css
/* En el siguiente codigo ocultaremos los formulario que sean hijo directos de un elemento de clase 'desabilitado' */

.deshabilitado > form {
    display: none;
}
```

### 2.2.4 Selector hermano siguiente
Es utilizado para asignarle estilo al hermano(del arbol DOM) que le sigue inmediatamente al primer elemento. Este lo hacemos a traves de el operador mas(+) Ejemplo:
```css
/* Si el elemento que sigue despues de un h1 es un parrafo este tendra una fuente color rojo */

h1 + p {
    color: red;
}
```

### 2.2.5 Selector hermanos siguientes
Es utilizado para asignarle estilo a **todos** los hermanoz(del arbol DOM). Este lo hacemos a traves de el operador mas(~) Ejemplo:

```css
/* Todos los hermano de h1 que sigan despues de el y  tengan la clase bg-black tendra una un fondo negro */

h1 ~ p {
    background: red;
}
```
## 2.3 Selectores de atributos
La forma de utilizar estos selectores es por medio de los corchetes( [] ). Exites varias maneras de hacer la implementacion:

### 2.3.1 Atributo y valor
Los hacemos de la misma manera como seria en codigo *HTML* pero esta vez encerrandolo en corchetes. Tambien podemos escribir solo el atributo sin espeficicar el valor. Ejemplo:
 ```css
 /* El siguiente codigo le coloca un fondo rojo y letras blancas a un button de tipo submit */

 [type='submit'] {
     background: red;
     color: white;
 }
 
 /* Se le asigna un borde solido rojo de un pixcel a los elementos de tipo requeridos */

 [required] {
     border: 1px solid red;
 }
 ```

 **NOTA:** Podemos utilizar notaciones para escapar caracteres. entre las opciones disponibles tenemos:

- Selecciona todos los elementos que su atributo href **comiencen** con losvalores /
```css
[href^='/'] {
    /* Asignacion de estilos */
}
```

- Selecciona todos los elementos que su atributo href **terminen** con los valores .jgp
```css
[href$='.jpg'] {
    /* Asignacion de estilos */
}
```

- Selecciona todos los elementos que su atributo class **contine** el valor button-
```css
[href*='button-'] {
    /* Asignacion de estilos */
}
```

- Selecciona todos los elementos que su atributo class **contine(separado por espacios)** el valor btn
```css
[href~='btn'] {
    /* Asignacion de estilos */
}
```

# 3 Especificidad
Al crecer nuestro codigo css es muy probable que tengamos problemas al asignarle dos estilos distintos a un mismo elemento. Esto es muy comun cuando utilizamos librerias de 3eros en nuestro codigo. Aqui es donde entra en juego la especificidad, que trata de ¿que tan espeficico es el selector que utilizamos?. Esto se calcula a traves de una suma, a continuacion una tabla con los elementos y su valor. El selector con mayor espeficidad gana.

| Elemento   | Valor                           |
| -----------|--------------------------------:|
| Tag        | 1                               |
| clases     | 10                              |
| id         | 100                             |
| inline     | 1000                            |
| !important | Es el dios (no debe utilizarce) |

**NOTA:** los selectores deberia ir escalando en su espeficidad a medida que crece el proyecto para evitar bugs.

# 4 Cascada y Herencia
Los que esta despues sobre escribe a lo que estaba antes. Tomando en cuenta que ambos selectores tienen la misma especificidad.

Todos los elementos heredan estilos de sus padres, abuelos, y su asendencia. Estos son los estilos que se mostraran por defecto a menos que sean sobre escritos por el mismo. La herencia funciona como una cascada en el arbol DOM.

**NOTA:** existen dos *keywords* que son **initial** y **inherit** que pueden  ser utilizadas como valor y lo que hacen respectivamente es inicializar(al valor por defecto) y forzar la herencia del padre respectivamente.

# 5 Box Model

## 5.1 Introduccion
El Box Model es el algoritmo a traves del cual el navegador dibuja las cajas en la pantalla. Para hablar del box model debemos tener presente alguno conceptos base:
### 5.1.1 Layout
Geometria de los elementosque se definen como, con que tamaño, com que separacion respecto a los elentos adyacentes y en que posicion se va adibujar en la pantalla.

### 5.1.2 Elemento en linea y de bloque.
Como ya debes saber HTML. Existen elemento de linea y de bloque por naturaleza. Nosotros en CSS podemos modificar la naturaleza de estos elementos(modificando su propiedad display). Algunas caracteristicas de estos elementos son las siguientes:

1. **Inline:** 
    - No crean nuevas lineas para cada elemento(los elementos se ajustan uno a los lados de los otros).
    - No se les puede definir un alto ni un ancho. Este es automatico.
    - Se ajustan a su contenido.

2. **Block:**
    - Crean una nueva linea para cada de elemento.
    - Ocupan todo el espacio horizontal disponible
    - Se les puede definir un alto y un ancho.

En CSS tenemos un tercer tipo de elemento que es el **inline-block** que combina lo mejos de ambos mundo:
- Tienen un alto y ancho que puede ser modificado.
- No crean nuevas lineas para los elementos.

## 5.2 Box Model
El box model trata justamente del modelo o modelado de las cajas(ya imaginaras que este es un elemento de caja)

**NOTA:** existe un atributo llamado **box-sizing**(sus valores son: *content-box*, *padding-box* y *border-box*).
Con el cual le indicamos al navegador que caja tendra los valores de *width* y *height* del elemento(por defecto este esta en *content-box*).

**NOTA IMPORTANTE:** Si el tamaño del alto del padre es automatico NO podremos utilizar porcentajes en el alto del elemento(no funcionara). Solo funcionan porcentaje en el alto del elemento si su padre tiene un alto definidos.
### 5.2.1 Caja de contenido
Content box. La definimos(por defecto, a menos que cambiemos el **box-sizing**) con las propiedades **width** y **height**.

### 5.2.2 Caja de relleno
Padding box. La definimos con la propiedad **padding**.
La implementacion es muy similar a la del margin(seccion 5.2.4). Aun asi una diferencia **importante** a la hora de trabajar con porcentajes en el padding es que este toma como referencia al inverso del papa. Es decir que cuando si el padre de nuestro elemento tiene un ancho de 200px y hacemos `padding-bottom: 10%` lo que estamos diciendo es que asigne al elemento un padding abajo de 20px. Esto lo podemos utilizar para hacer diseños a escaja.

### 5.2.3 Caja del Borde
Border box. La definimos con la propiedad **border**.

### 5.2.4 Margin
Separacion de la caja con las cajas adyacentes.
#### 5.2.4.1 Propiedades
Las propiedades que se encanrgan de modificar los valores del margen son:

- **margin-top:** Valor_superior
- **margin-right:** Valor_derecho
- **margin-botton:** Valor_inferios
- **margin-left:** Valor_izquierdo

Ademas exites de un shorthand que es:

- **margin:** el shorthand acepta de 1 a 4 valores. a continuacion una tabla que indica como son asignados los valores

| N° Valores | Arriba | Derecha | Abajo | Izquiera |
|------------|--------|---------|-------|---------:|
| 4          | 1ero   | 2do     | 3ero  | 4to      |
| 3          | 1ero   | 2do     | 3ero  | 2do      |
| 2          | 1ero   | 2do     | 1ero  | 2do      |
| 1          | 1ero   | 1ero    | 1ero  | 1ero     |

**NOTA:** Los valores pueden ser en pixceles o en porcentaje. Tambien existe la opcion de colocar *auto*.

# 6 Bordes y Sombras

## 6.1 ¿Donde se Dibuja?
El borde se dibuja siempre por dentro de la caja, recordemos que el unico elemento externo del model box es el margen.
**NOTA:** una buena practica recordemos que es aconfigurar el `box-sizing: border-box;`. De esta manera no evitamos problemas con el maquetado ya que aunque el borde esta por dentro de nuestra caja si no hacemos esta configuracion ñe aumentara las dimensiones a la misma.

## 6.2 Propiedades bases
El borde tiene 3 propiedades bases:
### 6.2.1 border-width
Configura el grosor de la linea.
### 6.2.2 border-style
Indica el estilo que se le aplicara a la linea. Sus posibles valores son:
- none(por defecto).
- hidden.
- solid.
- dotted.
- dashed.
- double.
- groove.
- ridge.
- inset.
- outset.

### 6.2.3 border-color
EL color de la linea.

### 6.2.4 Shorthands
Existen distintos shortand para los border:

1. **border:** *width_value* *style_value* *color_value*
2. **border-top:** *width_value_top* *style_value_top* *color_value_top*
3. **border-right:** *width_value_right* *style_value_right* *color_value_right*
4. **border-botton:** *width_value_botton* *style_value_botton* *color_value_botton*
5. **border-left:** *width_value_left* *style_value_left* *color_value_left*
6. **border-width:** *width_value_top* *width_value_right* *width_value_botton* *width_value_left*
7. **border-style:** *style_value_top* *style_value_right* *style_value_botton*
*style_value_left*
8. **border-color:** *color_value_top* *color_value_right* *color_value_botton*
*color_value_left*

## 6.3 border-radius
Esta propiedad nos permite "recordar" un arco de circunferencia(de 45°) en las esquinas de nuestras cajas. 

La sintaxis es la siguiente:

- **border-top-left-radius:** *x_radius y_radius*;
- **border-top-right-radius:** *x_radius y_radius*;
- **border-botton-right-radius:** *x_radius y_radius*;
- **border-botton-left-radius:** *x_radius y_radius*;
- **border-radius:** *x_radius_top_left x_radius_top_right x_radius_botton_right x_radius_botton_left / y_radius_top_left y_radius_top_right y_radius_botton_right y_radius_botton_left*;

**NOTA:** Los valores de los radios pueden darse en *px* o en *%*

## 6.4 outline
Funciona muy parecido al borde, con la diferencia que se dibuja por fuera de la caja. si sixtaxis es: `outline: width_value style_value color_value`

## 6.5 box-shadow
Los sombras son una de las caracteristicas mas facinantes de ccs. Todo esta en practicar y experimentar con ellas. sintaxis: `box-shadow: x-off y-offset blur spread color | inset(optional)`

# 7 Fondos
El background es una propiedad muy completa en css, sus propiedades son mostradas a continuacion.

## 7.01 Color
La propiedad es tan sencilla como puede ser posible, su sintaxis es: `background-color: color_value;`

## 7.02 Image
Sintaxis: `background-image: url(PATH)`

## 7.03 Repeat
Sintaxis: `background-repeat: value`

Posibles valores:
- repeat (por defecto)
- no-repeat
- repeat-x
- repeat-y

## 7.04 clip
Indica que parte de la caja es cubierta por el fondo.
Sintaxis: `background-clip: value`

Posibles valores:
- border-box(por defecto)
- padding-box
- content-box

## 7.05 origin
Indica desde parte caja se comienza a dibujar el fondo.
Sintaxis: `background-origin: value`

Posibles valores:
- border-box(por defecto)
- padding-box
- content-box

## 7.06 size
Nosotros podemos modificar el tamaño a mostrar de una imagen con ccs. La sintaxis de esta propiedad es: `background-size: value`

Posibles valores:
- widht=height (un solo valor puede ser en px o %)
- widht height (dos valores pueden  ser en px o %)
- contain (ajusta la imagen para que se muestre completa lo mas grande posible)
- cover (ajusta la imagen para que se muestre en el 100% de la caja, sin deformar la imagen)
- auto (esta es la opcion por defecto, muestra la imagen en su tamaño origina)

## 7.07 position
Esta propiedad es utilizada para especificar desde que coordenada se dibujara la imagen(la coordenadad [0,0] es igual a [left,right]). Sintaxis: `background-position: value`

Posibles valores:
- x (y se pone automaticamente, Puede ser en px o %)
- x y (Puede ser en px o %)
- left | center | right <unit> top | center | bottom <unit>

## 7.08 attachment
Esta propiedad nos permite  espeficicar la manera de mantener una imagen en el fondo.
Sintaxis: `background-attachment: value`

Posibles valores:
- scroll (por defecto)
- fixed
- local

## 7.09 multiples
Es pusible tener multiples fondos en una sola caja. Para manipular las propiedades de cada imagen las dividimos a traves de comas(,) comenzando por la url. Ejemplo:
```css
body {
    background-image: url(PATH_image1), url(PATH_image2), url(PATH_image3);
    background-size: 10%, 50 px, content;
}
```

## 7.10 shorthand
la sintaxis del shorthand es la siguiente:
`background: image position / size repeat attachment origin clip`

Los valores pueden ir en cualquier posicion menos las propiedades **position / size** estas si deben ir en este orden especifico. Position seguido del size separaados por un /.

# 8 Textos

## 8.1 Unidades
### 8.1.1 em
Es el tamaño de fuente del contexto(es variable depende del padre)
**NOTA:** Si el padre es el body, em=rem.

### 8.1.2 rem
Es el tamaño de fuente del root(es ctte depende del html)

## 8.2 Alineacion
### 8.2.1 Direction
Nos permite cambiar la direccion del texto. Su sintaxis es la siguiente: `direction: value;`.

Sus posibles valores son:
- ltr (left to right)
- rtl (right to left)

### 8.2.2 Indent
Nos Permite modificar la indentacion de la primera linea de un texto.

Sintaxis: `text-indent: value;`

Valores en *px* y *relativos*(em o rem).

### 8.2.3 Align
Indica la alineacion del texto.

Sintaxis: `text-align: value`

Posibles Valores:
- start (tiene que ver con direccion)
- end (tiene que ver con la direccion)
- left
- center
- right
- justify (se considera mala practica. Se ve feo en algunas pantallas)

**NOTA:** Exite una propiedad que es *text-align-last* que es para justificar la ultima linea.

### 8.2.4 Line-height
Indica la altura de linea.

Sintaxis:`line-height: value`

Los valores pueden ser relativos(em [no hace falta colocar la unidad]) o cttes(px)

### 8.2.5 Alineacion vertical
Sintaxis: `vertical-align: value`

Posibles valores:
- baseline (por defecto)
- top
- middle
- bottom

## 8.3 Flujo del Texto
### 8.3.1 Letter spacing(Espaciado entre letras)
Sintaxis: `letter-spacing: Value`

El valor es relativo o ctte. Positivo o negativo
### 8.3.2 Word spacing(Espaciado entre palabras)
Sintaxis: `word-spacing: Value`

El valor es relativo o ctte. Positivo o negativo

## 8.4 Decoration
Nos permita dibujar lineas en el texto
### 8.4.1 line
Nos indica el donde se ubicara la linea. Su sintaxis es:
`text-decoration-line: value`

Posibles valores:
- underline
- overline
- line-through
- none

### 8.4.2 color
Nos indica el color de la inea a dibujar. Sintaxis:
`tect-decoration-color: value`

### 8.4.3 style
Nos indica el estilo de la linea(igual que en border). Sintaxis:
`text-decoration-style: value`

Posibes valores:
- none.
- hidden.
- solid.
- dotted.
- dashed.
- double.
- groove.
- ridge.
- inset.
- outset.

### 8.4.4 shorthand
Al igual que muschas propiedades en css existe un shorthand para decoration. Su sitaxis es: `text-decoration: value_line value_style value_color`

**NOTA:** pueden asignarse varios valores de linea(arria, abajo, tachado)

## 8.5 shadow

Ee muy simlar al shadow de las border. Sintaxis: `text-shadow: h-offset v-offset blur color`.

## 8.6 Espacios en blanco
Esta propiedad trata del espacio en blanco cuanto tipiamos el en el codigo. nos permite o no escapar los espacios en blanco y los saltos de linea.

Sintaxis: `white-space: value`

Posibles valores:
- normal (escapa saltos de linea y espacio en blanco)
- pre (no escapa nada)
- nowrap (escapa solo los espacios en blanco)
- pre-wrap (salta de linea y conserva espacios)
- pre-line(salta de linea y no conserva espacios)

## 8.7 Desbordamiento
Es util cuando los textos se 'desbordan' de las caja que los contiene

### 8.7.1 break
Divide la palabra y manda el resto a la siguiente linea. Sintaxis `wrop-break: value`

Posibles valores:
- normal
- break-all
- keep-all
### 8.7.2 wrap
Manda la palabra a la siguiente linea, sino cabe la pica. Sintaxis `wrop-wrap: value`

Posibles valores:
- normal
- break-word
### 8.7.3 overflow
Nos sirve para indicar que el texto continua pero no cabe en la caja(colocando 3 puntos). Sintaxis 
```css
div {
    overflow: hidden; // todo lo que se escapa de la caja se oculta
    text-overflow: ellipsis;
}
```

Posibles valores:
- normal
- break-word

## 8.8 Transformacion
Esta propiedad no sirve para pasar imprimir el texto en mayusculas o minusculas. Sintaxis: `text-transform: value`

Posibles valores:
- uppercase
- lowercase
- capitalize

## 8.9 Fuentes
### 8.9.1 Font-family
**Familias de fuentes genericas**
Las principales familias de fuentes son:

1. **serif**
2. **sans-serif**
3. **monospace**
4. **display**
5. **cursive**

Sintaxis: `font-family: option1, option2, option3, familia_generica;`

### 8.9.2 Tamaño
Sintaxis: `font-size: value;`

Posibles valores:
- porcentaje
- pixeles
- em
- rem
### 8.9.3 Grosor del trazo
Sintaxis `font-weight: value`

Posibles valores:
- bold
- normal
- lighter
- bolder

**NOTA:** No es recomendable utilizar las palabras como valores. Lo recomentado es utilizar multiplos de 100 comprendidos entre 100 y 900

# 9 Pseudoclases
Estilos especiales dependiendo del conexto, posicion o estado.

En su sintaxis vemos el nombre del elemento seguido por dos puntos (:) y luego el nombre de la seudoclase. Ejemplo: `article:hover {...}`
Algunas seudoclases son:

## 9.1 root
Es una seudoclase que es equivalente al nodo *html* es decir, es el nodo principal. Es muy parecido al selector *html*, execto que su nivel de especificidad es mayor. Sirve para declarar variables CSS.

## 9.2 hover
Se presenta cuando el usuario coloca el puntero sobre algun elemento, pero no necesariamente esta activo. En pantallas touch *:hover* es problematico.

## 9.3 active
Esta cubre el caso en el que un elemento esta siendo activado por el usuario. Cuando se interactua con el raton. Corresponde al momento en el que el usuario presiona el raton hasta el momento en que lo suelta. A menudo es usado en los elementos <\a> y <\button> de HTML.
El **orden** si **importa** al momento de declarar las siguientes Pseudo-clases:
1. :link{ ... }
2. :visited { ... }
3. :hover { ... }
4. active { ... }

## 9.4 target
Representa un elemento unico, si existe alguno.
El id del elemento debe conincidir con el identificador de fragmentos de la URI del documento(href="#idOfElement")

## 9.5 child
Hay 3 tipos de hijos y estos hacen referencia al enesimo, al primero y al ultimo respectivamente:

### 9.5.1 nth-child()
Selecciona al elemento indicado que sea el n-esimo hijo de su elemento padre.

**NOTA:** Si el atributo es (3n). los estilos indicados seran aplicados cada 3 hijos. Si es (odd) Sera aplicado a los elementos pares. Si es (even) Sera aplicado a los elementos impares.
### 9.5.2 first-child
Selecciona al elemento indicado que sea el primer hijo de su elemento padre
### 9.5.3 last-child
Selecciona al elemento indicado que sea el ultimo hijo de su elemento padre

## 9.5 of type
Hay 3 tipos de, funcionan muy similar a las pseudoclases hijas y estos hacen referencia al enesimo, al primero y al ultimo respectivamente:

Puedes visualizar mejor las diferencias en [esta web](https://css-tricks.com/examples/nth-child-tester/)

### 9.5.1 nth-of-type()
Selecciona al elemento indicado que sea el n-esimo hijo de su elemento padre y del mismo tipo al elemento indicado.

**NOTA:** Si el atributo es (3n). los estilos indicados seran aplicados cada 3 hijos. Si es (odd) Sera aplicado a los elementos pares. Si es (even) Sera aplicado a los elementos impares.
### 9.5.2 first-child
Selecciona al elemento indicado que sea el primer hijo de su elemento padre y del mismo tipo al elemento indicado.
### 9.5.3 last-child
Selecciona al elemento indicado que sea el ultimo hijo de su elemento padre y del mismo tipo al elemento indicado.

## 9.6 not
La pseudo-clase de negacion, es una notacion funcional que toma un selector simple X como argumento. Coincide con un elemento que no esta representado por el argumento. X no debe contener otro selector de negacion. 
Es dicer, le aplicara los estilos a todos los elementos menos a los que se les espeficique con la pseudo-clase :not.

## 9.7 empty
Corresponde a un elemento sin ningun nodo hijo. Solo cuando hay nodos de elementos o texto con uno o mas caracteres dectro del elemento ese se convierte en no vacio. 

# 10 Pseudo-elementos
Son un tipo de "elementos falsos" pues en realidad estos no existen en el arbol DOM, sin embargo podemos manipularlos con CSS. Exiten varios, algunos de ellos son:

Son representados por el nombre del elemento, seguido de 4 punto(::) y luego el nombre del Pseudo-elemento.

## 10.1 Primera linea
Es util en textos y como su nombre lo indica hace referencia a la primera linea de texto mostrada en pantalla. Su sintaxis es la siguiente: `::first-line{ ... }`

**NOTA:** solo aplica para elementos de bloque.

## 10.2 Primera letra
Es util en palabras o textos y como su nombre lo indica hace referencia a la primera letra del texto mostrado en pantalla. Su sintaxis es la siguiente: `::first-letter { ... }`

**NOTA:** solo aplica para elementos de bloque.

## 10.3 before and after
- Son elementos *inline* por defecto.
- El contenido debe ser generado antes de ser manipulado.
Ejemplo:
```css
h1::before {
    content: 'Hola'; /* Inserta el string 'hola' delante del h1*/
}
h2::before {
    content: attr(class); /* Inserta el valor del atributo 'class' del elemento delante del mismo*/
}
h3::before {
    content: url(URI); /* Inserta la imagen de la ruta dada delante del elemento*/
}

.citas {
    quotes: '\201C' '\201D'; /*Estableces los caracteres abrir y cerrar de las citas(en este caso son caracteres UNICODE)*/
}

.citas::before {
    content: open-quote;
}

.citas::after {
    content: close-quote;
}
```
# 11 Listas y Contadores

## 11.1 Listas
Las listas tienen 3 propiedades en CSS:

**NOTA:** Podemos lograr que cualquier elementos "parezca" una lista con la propiedad `display: list-item`.

### 11.1.1 Tipo
El tipo o marca se refiere al tipo de viñeta que se le colocara o presedera a los elementos de las listas. Su sintaxis es:

`list-style-type: value`

Posibles valores:
- disc (circulo relleno)
- circle (circulo hueco)
- square (cuadrado relleno)
- decimal (numeros)
- decimal-leading-zero (numero con un cero por delante)
- lower-alpha (letras minusculas)
- upper-alpha (letras mayusculas)

### 11.1.2 Imagen
Exites una proiedad `list-style-image` pero es mala practica utilizarla. Es recomendable utilizar el pseudo-elemento ::before y colocar la imagen ensu background.

### 11.1.3 Posicion
Esta propiedad indica si las propiedades estar por fuera de los <\li> o por dentro. Sintaxis:`list-style-position: value`

Posibles valores:
- inside (dentro de los <\li>)

## 11.2 Contadores
Los contadores en css son muy parecidos a los contadores en un lenguaje de programacion.
Hay varias cosas a tener encuenta:
1. Deben ser declarados(en la propiedad *counter-reset:*)
2. Existen en el Scope que se les declara.
3. Se incrementan con la propiedad *counter-increment:*

Ejemplo
```css
.chapters {
    counter-reset: countOfChapters; /* Se inicializa/declara/resetea la variable a 0 */
}

.chapter {
    counter-increment: countOfChapters; /* Incremento el contador en cada elemento de la clase "chapter" */
}

.chapter::before {
    content: counter(countOfChapters) '.'; /* Imprimo el contador con un punto delante del elemento de la clase "chapter" */
}
```

**NOTA:** Para imprimir contadores en listas anidadas utilizamos la funcion de CSS *counters()* que recibe dos parametros el primero es el contador y el segundo es un string('') con el separador, ejemplo: `counters(countOfChapters, '.')`

# 12 Colores y degradados
## 12.1 Variables
En CSS tenemos una variable(se puede decir que es de las primeras que existio en el lenguaje), que hace referencia al valor de la propiedad *color* y estas es *currentcolor*.

## 12.2 Color keywords
Existen diferentes y muy variados keyword para los colores puedes verlos aca:

- **[Colores Basicos](https://www.w3.org/wiki/CSS/Properties/color/keywords)**

- **[Colores X11](https://en.wikipedia.org/wiki/X11_color_names)**

- transparent

## 12.3 Modo de color RGB
Caracteristicas:
- El modo RGB es un modo de color aditivo(de luz).
- Se basa en 3 canales; Rojo(R), Green(G), Blue(B).
- Su valores van de 0 a 255 (1 Byte).
- Los 3 canales en 255 dan blanco.
- Los 3 canales en 0 dan negro.
- Los 3 canales en el mismo nivel dan un tono de gris.

### 12.3.1 Diferencia entre rgb y rgba
La unica diferencia es que RGBA tiene un valor adiconal que hace referencia a alpha(transparencia), este valor va de 0 a 1(es un float).

### 12.3.2 Notacion hexadecimal
Es otra forma de denotar el modo de color:
    #RRGGBB

- Cada par de caracteres representa un canal.
- Si los dos caracteres de un canal se repiten puede abreviarse:
    #AA00EE = #A0E

## 12.4 Modo de color HSL
IMPORTANTE: **HSL no es HSB**.
### 12.4.1 ¿Que significa el acronimo?
- **Hue**(tonalidad de color,de 0 a 360, circulo cromatico).
- **Saturacion**(intensidad del color, de gris[0%]al color puro [100%]).
- **Luminosidad**(de negro [0%], color puro [50%], blanco[100%]).

### 12.4.2 Notacion hsl yhsla
- hsl(numero, porcentaje, porcentaje)
- hsla(numero, porcentaje, porcentaje, transparencia)

## 12.5 Degradados
En esencia **son imagenes**. Por lo tanto cuenta todas sus propiedades(background-size, position, etc).

### 12.5.1 Lineales

Sintaxis(lo que esta entre [] son parametros opcionales): `linear-gradient([angle], color1 [stop], colo2[stop], ..., colorN[stop])`

#### 12.5.1.1 Parametros opcionales:

##### 12.5.1.1.1 Angulo:
La unidad de los grados es *deg*.
Los grado son empezados a contar desde el eje vertivar(como los grados en topografia)
##### 12.5.1.1.1 Stops:
Son un porcentaje o tamaño fijo, e indican en donde el color se empieza a degradar. Ejemplo:
```css
background-image:linear-gradient(red 50%, blue) /*desde el inicio hasta la mitad es rojo puro, desde la mitad hasta el final es un degradado desde el rojo hasta llegar al azul*/
```
### 12.5.2 Radiales
A primera instancia son muy parecidos en su sintaxis: `background-image: radial-gradient([size shape], [at xcenter ycenter], color1 [stop1], color2 [stop2], ..., colorN [stopN])`

#### 12.5.2.1 Shape
Tiene dos posibles valores:
- circle
- elipse
**NOTA:** Si se omite la fomra se calcula por el tamaño del elemento.

#### 12.5.2.2 Size
Pueden ser unidades fijas o relativas(x y)

Existen algunas keywords que podemos utilizar:
- closet-side
- farthest-side
- closet-corner
- farthest-corner

#### 12.5.2.3 Repeat
Sintaxis: `repeat-radial-gradient([size shape], [at xcenter ycenter], color1 stop1, color2 stop2, ..., colorN stopN)`

# 13 Position
Nos permite posicionar un elemento alterando como se muestra el flujo de elementos.

## 13.1 Propiedad offset
Mueven un elemento posicionado segun el borde indicado, sus sintaxis son:
- `top: value`

- `right: value`

- `left: value`

- `bottom: value`

## 13.2 Valores de posicion
Exiten varios tipos que nos permiten modificar el posicionamiento de un elemento, su sintaxis es:

`position: valuePosition`

### 13.2.1 Static
Es el valor por defecto que tienen los elemento, Mantienen el posicionamiento por el flujo del HTML. A los elemento con ese valor no se les considera posicionados.

### 13.2.2 Relative

Caracteristicas:
- Su referencia es su posicion inicial.
- Aplicar `position: realtive` a un elemento no modifica en nada su layout.
- Al moverlo, con las propiedades offset, reserva su espacio.

### 13.2.3 Absolute
Caracteristicas:
- Pierde su posicion en el flujo y no reserva su espacio.
- Si tenia dimensiones fijas se mantienen, si tiene dimensiones automaticas; se ajustaran a su contenido.
- Su referencia es su ancestro *posicionado* mas cercano.

### 13.2.4 Fixed
Caracteristicas:
- Fijo(no se mueve con el scroll), relativo al viewport.
- Se ignora en el flujo.
- Sus dimensiones automaticas se restringen a su contexto.

### 13.2.5 Sticky
Es una combinacion de Relative y Fixed.
En este caso el *offset* indica en que instante el elemento pasara a ser fijo en pantalla. Ejemplo para un `top: 10px`. El elemento sera fijo cuando al hacer scroll este saliendo de pantalla, y se mantendra a *10px* del viewport en su parte superior.

# 14 z-index
Si nos imaginamos el origen de coordenadas en las esquina superior izquierda de nuestro computador. A medida que aumentamos coordenadas en z estas esta 'mas cerca de nosotros', Asi que podriamos decir que que los elementos con menor z-index(coordenadas en z) seran sobrepuestos por aquellos con un z-index mayor.

- Por defecto *todos* los elemmentos tienen z-index = 0.
- Para elementos con igual z-index se sobrepondran aquellos que aparezcan despues en el flujo(codigo HTML).

Una estructura recomendada por el equipo de [EDteam](https://ed.team) es:
```css
    --z-back    : -10;
    --z-normal  : 1;
    --z-tooltip : 10;
    --z-fixed   : 100;
    --z-modal   : 1000;
```

Como ves es una buena practica utilizar una escala que nos permita tener valores intermedios para manejar nuestros valores, de una forma mas legible y practica

Elementos aplicables:
- Elementos posicionados.
- Elementos Transformados.

NOTA: si el papa tiene un z-index declarado el/los hijo(s) no pueden posicionarse detras de el.

# 15 Flexbox
Su principal funcion es de alineacion. Si bien podemos realizar algo del layout con este, solo podemos hacerlo en un solo eje(main axis).
Utiliza siempre la relacion padre e hijos. No puede existir un flexbox sin este contexto.

Los elementos padre son llamados **flex container** y tienen la propiedad **display: flex**

## 15.1 Ejes

Tenemos dos ejes:
- Eje principal(main axis): De manera predeterminada el eje principal es horizontal, de izquierda a derecha.

- Eje transversal(cross axis): De manera predeterminada es vertical, de arriba hacia abajo.

## 15.2 Flex Container(Padre)

### 15.2.1 Display
El flex container(El padre) tiene dos opciones en su display:

1. `display: flex`. Se comporta como un elemento de bloque.
2. `display: inline-flex`. Se comporta como un elemento de linea.

### 15.2.2 Flex-direction
Flex-direction nos permite especificar la direccion y el sentido del eje principal:

#### 15.2.2.1 Sintaxis
`flex-direction: value;`

#### 15.2.2.2 Valores posibles
- row (Predeterminado)
- row-reverse (Horizontal, de derecha a izquierda)
- column (Vertical, de arriba a abajo)
- column-reverse (Vertical, de abajo a arriba)

### 15.2.3 Flex-wrap
Esta propiedad no especifica si el flexbox puede o no saltar de linea:

#### 15.2.3.1 Sintaxis
`flex-wrap: value`

#### 15.2.3.2 Posibles Valores
- nowrap(los hijos no pueden saltar de linea. Por defecto)
- wrap (los hijos pueden saltar de linea)
- wrap-reverse (los hijos pueden saltar de linea. Las lineas estan en el orden opuesto[el eje trasversal esta en reversa]).

### 15.2.4 Flex-flow
Es un shorthand que une a *flex-direction* y a *flex-wrap*.

Sintasis: `flex-flow: value_direction value_wrap`

### 15.2.5 Alineacion

#### 15.2.5.1 Alineacion de Items

##### 15.2.5.1.1 Justify-content
Alinea los Items en el eje principal(main axis)
Sintasis:
`justify-content: value`

Posibles Valores:
- flex-start (Predeterminado)
- flex-end
- flex-center
- space-between
- space-around(Es parecido a un margen automatico)
- space-evenly

##### 15.2.5.1.2 Align-items
Alinea los Items en el eje transversal(cross axis) dentro de la linea
Sintasis:
`align-items: value`

Posibles Valores:
- flex-start (Predeterminado)
- flex-end
- flex-center
- baseline
- stretch

#### 15.2.5.2 Alineacion de Lineas
##### 15.2.5.2.1 Align-content
ALinea las lineas respecto al container

Sintasis: 
`align-content: value`

Posibles valores:
- flex-start (Predeterminado)
- flex-end
- flex-center
- space-between
- space-around
- space-evenly
- stretch

## 15.3 Flex Items
Los siguientes elementos son catalogados como items:
- Hijos directos.
- Pseudoelementos.
- Texto

### 15.3.1 Flex items posicionados
Los elementos posicionados con absolute o fixed tienen las siguientes caracteristicas:

- No participan en el flujo.
- Son afectados por las propiedades de alineacion del container.

### 15.3.2 Crecimiento o reduccion
Los flex items pueden crecer(grow) o reducirse(shrink). Algo a tener en cuenta es que los margenes y paddings no se contraen

### 15.3.3 Propiedades

#### 15.3.3.1 flex-grow
Flex-grow Indica el factor de crecimiento.

- El Navegador Calcula el espacio disponible. Tomando en cuenta el tamaño inicial de cada elemento.
- El navegador divide el espacio disponible entre la cantidad total de los factores de crecimiento.
- Se le asigna a cada elemento el tamaño corespondiente a la cantidad de factores de crecimiento establecidas para el mismo.

Sintaxis:
`flex-grow: valor_del_factor_de_crecimiento`

Valores Posibles:
- Numero positivos(enteros o decimales). Por defecto es 0.

#### 15.3.3.2 flex-shrink
Flex-shrink Indica el factor de reduccion.

- El Navegador Calcula el espacio sobrante. Tomando en cuenta el tamaño inicial de cada elemento.
- El navegador divide el espacio sobrante entre la cantidad total de los factores de reduccion.
- Se le reduce a cada elemento el tamaño correspondiente a la cantidad de factores de reduccion establecidos para el mismo.

Sintaxis:
`flex-shrink: valor_del_factor_de_reduccion`

Valores Posibles:
- Numero positivos(enteros o decimales). Por defecto, se distribuye uniformemente entre todos los elementos.

#### 15.3.3.3 flex-basis
Define el **tamaño inicial en el eje principal** puede ser width o height dependiendo del caso.

**IMPORTANTE:** Cuando esta asignado ignora la propiedad width o height(dependiendo del caso de como este configurado el eje principal).

Sintaxis:
`flex-basis: value`

Posibles valores:
- Recibe los mismos valores que una propiedad *size*.

#### 15.3.3.4 Flex
Flex es un shorthand que agrupa a **flex-grow**, **flex-shrink** y **flex-basis**

**Sintaxis:**
`flex: value-grow value-shrink value-basis`

**Keywords:**

- initial (0 1 auto). Estos son los valores por defecto.
- auto(1 1 auto)
- none(0 0 auto)
- n (n 0 0). Siendo *n* un numero positivo.

#### 15.3.3.5 aling-self
Nos sirve para linear un items en especifico. Lo podriamos utilizar en conjunto con la pseudoclase *nth-child()*.

Sintasis:
`align-self: value`

Valores Posibles:
- auto(por defecto. Sigue el flujo definido en el contenedor)
- flex-start
- flex-end
- center
- baseline
- stretch

#### 15.3.3.6 Order
Nos permite colocar un elemento en la parte que deseemos. Sin importar el flujo del HTML.

Se parece un poco a un *z-index*. Por defecto todos los elemento tienen un order:0.

Sintaxis:
`order: value`

Valores posibles:
- Cualquier numero entero.

# 16 Grid
- Permite construis layouts a traves de dos ejes(horizontas y v ertivas | inline y block)).
- No importa la posicion de un elemento en el codigo HTML para construir el layout.
- Requiere un relacion de padre(grid-container) e hijos(grid-items)

## 16.1 Grid-container
### 16.1.1 display
**Valores:**
- grid.(Visualmente no altera en nada al elemento, es como si aplicaramos un position:relative).

- inine-grid.

## 16.2 Elementos abstractos(no existen en el DOM)
Son definidos en las propiedades del grid-container.
### 16.2.1 Grid-tracks
Son las filas y las columnas.

#### 16.2.1.1 Definiendo Tracks
##### 16.2.1.1.1 Columnas
Sintaxis:
`grid-template-columns: width_column1 width_column2 ... width-columnN`

Los valores adminitos:
- Son cualquier valor para definir tamaño(em, rem. px, %).
- fr: Son definidos como valores fracionarios. Tienen un comportamiento muy similar al valor de flex-grow.


##### 16.2.1.1.2 Filas
Sintaxis:
`grid-template-rows: width_row1 width_row2 ... widthrowN`

Los valores adminitos:
- Son cualquier valor para definir tamaño(em, rem. px, %).
- fr: Son definidos como valores fracionarios. Tienen un comportamiento muy similar al valor de flex-grow.

##### 16.2.1.1.2 Gap
Espeficican la separacion entre columnas o filas respectivamente:
Columnas:
`grid-column-gap: value`

Filas:
`grid-row-gap: value`

Posibles valores:
- Unidades fijas o relativas.

Shorthand:
`grip-gap: value_row value_column`

### 16.2.2 Grid-lines 
Se encuentran a los lados de los tracks:
- Izquierda y derechas para columnas.
- Arriba y abajo para filas.
### 16.2.3 Grid-cells
La Interseccion entre una fila y una columna.
### 16.2.4 Grid-areas
Cualquier area rectangular delimitada por 4 *grid-lines*

## 16.3 Grid-items
Se consideran como grid-items a los:
- Hijos directos
- Pseudoelementos ::before y ::after
- Texto

### 16.3.1 Posicionamiento
Con css-grid podemos colocar un elemento donde queramos. Esto lo hacemos especificandole la linea donde inicia y donde termina dicho elemento.
Para esto utilizamos las porpiedades:
```CSS
.element {
    grid-column-start: value;   /* Linea vertical inicial */
    grid-row-start: value;      /* Linea horizontal inicial */
    grid-column-end: value;     /* Linea vertical final */
    grid-row-end: value;        /* Linea horizontal final */
    
    /*
    Shorthands
    grid-row: value_start / value_end;
    grid-column: value_start / value_end;

    Nota: tambien podemos contar columnas o filas, utilizando las unidad 'span'. Ejemplo. una grilla que ocupe desde la linea 1 hasta la cuarta columna:
    grid-column: 1 / span 4; 
    */
}
```
**NOTA1:** Los grid-items pueden ser a su vez grid-containers.

**NOTA:2** Los grid container tambien manejan las propiedades  *justified-content* y *aling-items*.

## 16.4 Alineacion

### 16.4.1 Items
Estas alineaciones son para alinear el contenido de cada track. Las propiedades son muy parecidas a las de flex.

En horizontal(x o inline) tenemos las propiedades:
- justift-items (todos)
- justify.self (uno en particular)
 
En Vertical(y o block) tenemos las propiedades: 
- align-items (todos)
- aling-self (uno en particular)

**NOTA:** Tambien se pueden utilizar margenes para alinear elementos.

### 16.4.2 Container
Estas propiedades las utilizamos para mover la alineacion de los tracks respecto al contenedor. Las propiedades son muy parecidas a las de flex.

En horizontal(x o inline) tenemos las propiedades:
- justift-content
 
En Vertical(y o block) tenemos las propiedades: 
- align-content

## 16.5 Placement
Exites dos clases de Grid:

- Explicitos: Aquellos que definimos en la grilla, con grid-template.

- Implicitos: Aquellos que el navegador crea automaticamente cuando ya hemos llenado nuestra grilla totalmente.

Por defecto los elemento implicitos se ajustan a su contenido. Podemos definir su tamaño con.

```CSS
.container {
    grid-auto-rows: value_size;
    grid-auto-colums: value_size;

    grid-auto-flow: value [dense]; /* Valores: row(predeterminado) | column. Esta propieda especifica algo asi como el eje principal.
    
    *dense* es un valor opcional. Es utilizado para llenar huecos en la grilla en el dado caso de que haya un salto de linea por un columna que hayamos fijado.
    */
}
```

# 17 Transfromaciones

## 17.1 Transfromaciones en 2D

### 17.1.1 Coordenadas
- X (Horizontal, izquierda hacia derecha).
- Y (Vertical, arriba hacia abajo).

El punto (0,0) es la esquina superior izquierda.

Propiedad:
- `transform-origin: x y`. Nos indica el origen de coordenadas para escalar y rotar un objeto, NO para trasladar. Su valores son cualquier unidad de tamaño y las keyword: left, right, bottom, top.
### 17.1.2 Funciones transformacion
Importante: El especio disponible del elemento transfromado siempre queda reservado.

- Translate:
`translate(x | x,y) | translateX() | translateY()`

- Scale:
`scale(x=y | x,y) | scaleX() | scaleY()`

- Skew:
`skew(x | x,y) | skewX() | skewY()`

- Rotate: `rotate(<angle>)`.
    Unidades de rotacion: 
    - deg(360deg)
    - grad(400grad)
    - rad(6,2832rad)
    - turn(1turn)


## 17..2 Transformaciones en 3D

# 18 Animaciones

## 18.1 Triggers
Los triggers son los cambios que ocurren en el navegador cuando una porpiedad de CSS es cambiada.

Cuando se cambia una propiedad CSS, el navegador necesita reaccionar a ese cambio. Los tipos de cambios son de mayor a menor costo de recursos:

1. Layout: Geometria y posicion de los elementos(muy costoso en recursos)

2. Paint: Pintar los pixeles de los elementos(Cuesta menos que el layout pero de igual manera consume muchos recursos).

3. Composite: Combina y dibuja las capas en pantalla(es el mas liviano de todos)
    - Solo opacity y transform desencadenan composicion.
    - Se fea una capa que almacena al objeto y solo esa capa es transformada(en lugar de repintar todos los elementos).

Puedes observar con mas detalle la lista de elementos disparadores [acá](https://csstriggers.com). 

NOTA: Existe una extension de VScode llamada css-triggers muy util. Esta basada en la lista del link de arriba.

## 18.2 Valores iniciales
Todas las porpiedades CSS tiene un valor inicial por defecto, asi no se lo asignemos. Este valor debe ser numerico para que para que pueda ejecutarse la animacion. De lo contrario el navegador no pueder calcular los valores intermedios de la animacion.

NOTA: Hay elementos animables y otro que no lo son. Buscar tabla en MDN.

## 18.3 Transiciones
Las transiciones son los cambios(transiciones) que ocurren de una propiedad a otra en un determinado periodo de tiempo.

### 18.3.1 Caracteristicas

- Permiten que las propiedades CSS cam,bien suavemente en un periodo de tiempo determinado.
- Se pueden definir multiples transiciones separadas por comas.
Si los numeros de transiciones no coinciden con las multiples propiedades se hacen conincidir repitiendolas.

### 18.3.2 Propiedades
- nombre-propiedad: posible-valor | posible-valor | posible-valor | ...

1. `transition-property: all | none | propiedad[,propiedad]`

2. `transition-duration : 0s | time[,time]`. No se permiten valores negativos 

3. `transition-delay: 0s.`Indica cuando la transicion iniciara, por defecto es 0s.

4. `transition-timing-function: ease | linear | ease-in | ease-out | ease-in-out | step-start | step-out | steps()`. Como se calcula cada valor intermedio mientras dura la transción. Los **steps** Son muy utiles en el uso de sprites.

5. `transition: transition-property transition-duration- transition-delay transition-time-function`. Es un shorthand.

## 18.4 Animaciones
Permiten cambiar propiedades CSS a traves de momentos en el tiempo definidos como **keyframes**. A diferencia de las *transiciones* que requieren de un cambio de propiedad para ejecutarse, las animaciones ejecutan por si mismas esos cambios de propiedades.

### 18.4.1 Propiedades
Se pueden iniciar varias animaciones separandolas por comas.

**Propiedades minimas para animar:**
- propiedades: posible-valor(valor por defecto) | posible-valor[,valor-opcional] | posible-valor

1. `animation-name: none | nombre-animacion;`

2. `animation-duration: 0s | time;` No se aceptan valores negativos.

**Otras propiedades:**

3. `animation-iteration-count: 1 | number | infinite;` Acepta numeros no enteros.

4. `animation-timing-function: ease | ease-in |  ease-in-out |ease-out | linear | steps | cubic-bezier()`

5. `animation-direction: normal | reverse | alternate | alternate-reverse`

6. `animation-play-state: running | paused` Una animacion CSS no puede reiniciarse sin JS.

7. `animation-delay: 0s | time` Acepta valores negativos.

8. `animation-fill-mode: none | forwards | backwards | both`

9.  `animation: values` Es un shorthand. La unica condicion en el orden de valores es que *animation-duration* va primero que *animation-delay*

#### 18.4.1.1 CSS Timing Function

##### 18.4.1.1.1 Cubic-bezier()
Esta basada en una [curva bezier](https://link) como las utilizadas en programas de diseño para dibujar vectores.

Es un concepto usado para indicar una relacion entre valores. En este caso es una curva que controla la relacion tiemp/cambio en la animacion:
- Eje X(horizontal): Tiempo.
- Eje Y (vertical) cambio de propiedades.

**La Funcion cubic-bezier()** recibe cuatro parametros que son las coordenadas de los puntos de control de la curva:
- animation-timing-function: cubic-bezier(P1x, P1y, P2x, P2y)
- transition-timing-function: cubic-bezier(P!x, P1y, P2x, P2y)

Posibles valores:
- Los valores van de 0 a 1
- Pueden ser mayores que 1(o negativos) en el eje Y(nunca en X porque es el tiempo)creando interesantes efectos.

[Referencias](https://www.w3.org/TR/css-easing-1/)

[Herramienta en linea](https://cubic-bezier.com/#.17,.67,.83,.67). Loas navegadores tambien tienen un editor en las herramientas de desarrolladores
### 18.4.2 at-rule keyframes

```CSS
@keyframes nombre-animacion {

    porcentaje | from | to { /* from=0% y to=100%*/
        propiedad: valor;
    }

    50% { /* A mitad de la animacion llegara a este estado */
        propiedad: valor;
    }
    to { /* Al final de la animacion llegara a este estado */
        propiedad:valor;
    }

}
```

- Debe especificarse cada keyframe con el signo de %.
- Los keyframe actuan como selectores por lo cual pueden agruparse con comas.
- 0% no especificado: El navegador crea un keyframe 0% con los valores iniciales del elemento.
- 100% no especificado: El navegador crea un keyframe 100% con los valores iniciales del elemento.
- Las propiedades no animables cambian, pero sin animacion.
- No tienen cascada, por lo tanto una animacion nunca tomara keyframe de mas de una at-rule keyframes.

### 18.4.3 Controlar animaciones con JS
#### 18.4.3.1 Evento animation
Exites tres eventos con los cuales podemos interactuar desde Js con las animaciones en css:

- animationstart: Al inicio de la animacion.
- animationend: Al final de la animacion.
- animationiteration: Al comenzar una nueva animacion.
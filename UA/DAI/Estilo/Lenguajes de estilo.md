## Selectores y propiedades del lenguaje CSS

CSS (Cascading Style Sheets) es un lenguaje utilizado para describir la presentación de un documento HTML. Sus principales componentes son los **selectores** y las **propiedades**.

#### Selectores en CSS

Los **selectores** se utilizan para especificar qué elementos HTML serán estilizados. Existen varios tipos de selectores:

1. **Selector de tipo**: Selecciona todos los elementos de un tipo dado.
    
    `p {   color: blue; }`
    
    Aplica el estilo a todos los párrafos (`<p>`).
    
2. **Selector de clase**: Selecciona elementos con una clase específica, usando un punto.
    
    `.boton {   background-color: red; }`
    
    Aplica el estilo a cualquier elemento con `class="boton"`.
    
3. **Selector de ID**: Selecciona un elemento con un ID específico, usando `#`.
    
    `#menu {   width: 100px; }`
    
    Aplica el estilo al elemento con `id="menu"`.
    
4. **Selector universal**: Selecciona todos los elementos.
    
    `* {   margin: 0; }`
    
    Aplica el estilo a todos los elementos de la página.
    
5. **Selectores descendientes**: Selecciona elementos que son descendientes de otros elementos.
    
    `div p {   font-size: 16px; }`
    
    Aplica el estilo solo a los párrafos que están dentro de un `<div>`.
    
6. **Selectores de atributos**: Selecciona elementos en función de sus atributos.
    
    `input[type="text"] {   border: 1px solid black; }`
    
    Aplica el estilo a todos los elementos `<input>` con el atributo `type="text"`.
    

#### Propiedades en CSS

Las **propiedades** definen cómo se aplicará el estilo a los elementos seleccionados. Algunas de las propiedades más comunes incluyen:

1. **Propiedades de color**:
    
    - `color`: Establece el color del texto.
        
        `color: #333;`
        
    - `background-color`: Establece el color de fondo.
        
        `background-color: #f0f0f0;`
        
2. **Propiedades de texto**:
    
    - `font-size`: Tamaño de la fuente.
        
        `font-size: 14px;`
        
    - `font-family`: Fuente de texto.
        
        `font-family: Arial, sans-serif;`
        
    - `text-align`: Alineación del texto.
        
        `text-align: center;`
        
3. **Propiedades de caja (box model)**:
    
    - `margin`: Define el margen exterior de un elemento.
        
        `margin: 10px;`
        
    - `padding`: Define el espacio interior entre el contenido y el borde.
        
        `padding: 15px;`
        
    - `border`: Define el borde de un elemento.
        
        `border: 1px solid black;`
        
4. **Propiedades de disposición**:
    
    - `display`: Controla cómo se muestra un elemento (bloque, inline, flex, etc.).
        
        `display: block;`
        
    - `position`: Establece cómo se posiciona un elemento (relativo, absoluto, fijo, etc.).
        
        `position: absolute;`
        
5. **Propiedades de fondo**:
    
    - `background-image`: Establece una imagen de fondo.
        
        `background-image: url('imagen.jpg');`
        
    - `background-size`: Define el tamaño de la imagen de fondo.
        
        `background-size: cover;`
        

#### Conclusión

CSS permite dar estilo a los elementos HTML mediante el uso de **selectores** y **propiedades**. Los selectores permiten identificar elementos específicos en la página, mientras que las propiedades definen cómo se verán esos elementos. La combinación de ambos es lo que hace que una página web sea visualmente atractiva y funcional.

### Cálculo de especificidad

- un estilo aplicado en línea con el atributo `style` suma 1000 a la especificidad
    
- cada identificador (_id_) que aparezca en el selector suma 100
    
- cada selector de clase, de atributo o de pseudo-clase (`:hover`) suma 10
    
- cada elemento o pseudo-elemento (`::before`) suma 1

| Selector                       | Especificidad |
| ------------------------------ | ------------- |
| `p`                            | 1             |
| `div p`                        | 2             |
| `.menu`                        | 10            |
| `div ul.menu`                  | 12            |
| `#activo`                      | 100           |
| `body #contenido .principal p` | 112           |

### Elementos en línea y en bloque

Elementos en bloque:

- Su caja comienza en una nueva línea debajo de la caja anterior y, salvo que se restrinja explícitamente, se extiende completamente a derecha e izquierda hasta ocupar todo el ancho disponible para el elemento padre.
- La caja de cualquier elemento posterior también aparece en una nueva línea.
- La altura de la caja depende del contenido (si se estrecha la ventana del navegador, la caja se alarga convenientemente para que el contenido quepa en ella), aunque puede fijarse explícitamente con propiedades como `height`.
- Elementos como `<p>`,`<div>` o `<section>` son ejemplos de elementos de bloque; `<div>` es un elemento de bloque especial de HTML ya que no tiene una semántica asociada: su propósito es delimitar contenido cuya representación tiene algún estilo diferenciado, pero que no tiene un matiz semántico que se pueda representar mediante un elemento HTML.

En el caso de los elementos en línea:
- Estos elementos no se muestran en una nueva línea ni provocan la aparición de una nueva línea al final de ellos.
- Las cajas en línea no afectan al espaciado vertical.
- El ancho de su caja depende de su contenido (propiedades como `width` y `height` son ignoradas), no del ancho del elemento padre.
- Ejemplos de elementos en línea son `<strong>`, `<span>` o `<a>`; al igual que `<div>`, `<span>` no tiene semántica asociada y su propósito es el mismo que el de `<div>` pero para contenido en línea.

### Modelo de caja en CSS

Todos los elementos de HTML se muestran en una caja _imaginaria_ que se extiende alrededor de su contenido. Si bien el posicionamiento o el tamaño de estas cajas sigue reglas por defecto como las que hemos visto, muchas de estas propiedades geométricas pueden modificarse mediante reglas de CSS. Entender el modelo de caja de CSS es fundamental a la hora de dar estilo a una página web. Esto implica, entre otras cosas, entender bien la forma de definir los márgenes, el borde y el relleno (_padding_) de cada caja.

![[Pasted image 20240920102035.png]]

Esta es una lista de los principales parámetros de una caja que podemos modificar mediente propiedades de CSS:

- El ancho y alto de cada caja se pueden definir explícitamente mediante las propiedades `width` y `height`.
    
- Cada caja tiene un borde alrededor. El grosor de este borde se define con las propiedades `border-top-width`, `border-right-width`, `border-bottom-width` y `border-bottom-left`; estas propiedades suelen tener valor cero por defecto. El color del borde se define con las propiedades `bottom-top-color`, `bottom-right-color`, etc. El trazo del borde puede, además, mostrarse con una línea continua (`solid`), con una línea discontinua (`dashed`) o con una línea de puntos (`dotted`), entre otros; estos valores pueden asignarse a las propiedades `border-top-style`, `border-right-style`, etc.
    
- Cada caja tiene un relleno (_padding_), que es la distancia entre el borde y el contenido de la caja; este relleno se define con las propiedades `padding-top`, `padding-right`, etc.
    
- Por último, es posible definir los márgenes entre una caja y las cajas de alrededor mediante las propiedades `margin-top`, `margin-right`, etc.
    

Las separaciones y grosores anteriores se definen en base a las múltiples unidades de medida permitidas en CSS, como _píxeles_ o _ems_. Si el valor es cero, no es necesario indicar la unidad de medida (0 píxeles y 0 _ems_ es lo mismo en este caso).

Existen formas compactas de definir algunas de las propiedades anteriores. Así, la propiedad `padding: 3em 2em 1em 0` establece el relleno, por este orden, superior, derecho, inferior e izquierdo; la propiedad `padding: 2em 1em` establece los rellenos superior e inferior (rellenos verticales) a `2em` y el relleno derecho e izquierdo (rellenos horizontales) a `1em`; si solo tiene un valor, la propiedad `padding: 2em` establece todos los rellenos a `2em`. La propiedad `margin` puede tener un número variable de valores, al igual que `padding` y con la misma semántica. Existe también una propiedad para dar valor al grosor de varios bordes a la vez, pero no es `border` (un error bastante común), sino `border-width`. La propiedad `border` a secas cambia el grosor de todos los bordes, su estilo y su color a la vez, como en `border: 1px solid blue`.

![[Pasted image 20240920102742.png]]
![[Pasted image 20240920102759.png]]

De paso, hemos hecho que las medidas de todas las cajas se determinen usando el criterio `border-box`, lo que también constituye una buena práctica. Con el criterio por defecto, `content-box`, si se define el ancho de una caja en 100 píxeles, por ejemplo, la subcaja del contenido del elemento tendrá 100 pixeles de ancho y el ancho de cualquier borde o relleno especificado se sumará al ancho final reflejado; es por ello que las cajas del ejemplo anterior tiene tamaños diferentes. Esto provocaba hace años que a menudo los desarrolladores tuvieran que andar restando al ancho total deseado las medidas del borde y el relleno de cara a obtener el valor adecuado del atributo `width`. Con el valor `border-box` de la propiedad `box-sizing` la caja completa tendrá 100 píxeles de ancho y, si hay borde o relleno, la subcaja de contenido reducirá su tamaño para que el ancho final mostrado para la caja sea de 100 píxeles. Observa que los márgenes no modifican la caja con uno u otro valor de la propiedad, ya que no definen en sí propiedades de la caja del contenido sino del espacio entre ella y las cajas adyacentes.

#### Posicionamiento

Las opciones anteriores son bastante limitadas y es habitual que necesitemos más libertad a la hora de distribuir el contenido de los elementos en una página web. Una de las formas básicas de conseguirlo es a través del atributo `position`, que puede tener los valores `static`, `relative`, `absolute`, `fixed` y `sticky`.

#### Posicionamiento estático

El posicionamiento `static` corresponde al comportamiento por defecto que ya hemos visto: por ejemplo, cada elemento de tipo bloque se muestra en la línea siguiente al elemento anterior. Si un elemento no tiene asociado ningún valor en su propiedad `position` esta tomará el valor `static`.
![[Pasted image 20240920102936.png]]
![[Pasted image 20240920102950.png]]

#### Posicionamiento relativo

El posicionamiento `relative` nos permite cambiar la posición por defecto de un elemento, moviéndolo de la posición que le habría correspondido por defecto con ayuda de las propiedades `top`, `bottom`, `left` y `right`. Por poner un ejemplo, extensible a las otras tres propiedades, el valor de `left` es aquí la distancia del borde izquierdo de la ubicación donde se habría colocado la caja del elemento por defecto al borde izquierdo de la ubicación en la que finalmente se colocará. Si no se da valor a ninguna de estas cuatro proiedades, el elemento se mostrará exactamente en su lugar por defecto; como veremos más adelante, definir `position` como `relative`, aun sin cambiar ninguna de las propiedades `top`, `bottom`, `left` o `right`, puede ser muy útil para que un elemento se considere como _posicionado_ cuando usemos el posicionamiento de tipo absoluto.

Este posicionamiento es muy utilizado para realizar pequeños ajustes en la posición por defecto en la que se muestra un determinado elemento.
![[Pasted image 20240920103027.png]]

Observa cómo el espacio por defecto que ocupaba el cuadrado azul no ha sido ocupado por ningún otro elemento. Es como si el motor de visualización del navegador ignorara el posicionamiento relativo en una primera pasada y lo tuviera en cuenta en una segunda pasada tras haber colocado todos los elementos de la página.

![[Pasted image 20240920103125.png]]![[Pasted image 20240920103142.png]]

La propiedad `z-index` solo funciona si el elemento _está posicionado_. Diremos que un elemento _está posicionado_ si el valor de su posición es cualquiera excepto `static`. Por ello es por lo que hemos tenido que añadir un posicionamiento relativo a la caja lavanda (pero no hemos cambiado ninguna propiedad como `top`, `bottom`, `left` o `right` para no cambiar su posición).

Finalmente, observa cómo con el uso adecuado del posicionamiento relativo podemos cambiar el orden en el que se muestra la información en el navegador respecto al orden inicialmente definido en el documento HTML:
![[Pasted image 20240920103216.png]]


#### Posicionamiento absoluto

Si el posicionamiento `relative` que acabamos de ver permite colocar un elemento de forma relativa a su posición por defecto, el posicionamiento `absolute` permite colocarlo de forma relativa al elemento padre (más abajo matizaremos esto). En este caso, no _deja hueco_, porque nunca llega a tener una posición original propia. Además, de nuevo podemos usar las propiedades `top`, `bottom`, `left` y `right` para moverlo. Por poner un ejemplo, extensible a las otras tres propiedades, el valor de `left` es la distancia del borde izquierdo de la caja contenedora al borde izquierdo de la caja que resultará para el nuevo elemento. Un elemento con posicionamiento absoluto no influye en otros elementos ni otros elementos influyen en él.
![[Pasted image 20240920103252.png]]

Observa cómo además de añadir las propiedades `position`, `left` y `right` al elemento azul, hemos añadido `position: relative` al padre (esto es, al elemento contenedor). Esto es así porque las reglas son un poco más complejas que las mencionadas anteriormente: en realidad, el posicionamiento absoluto usa como referencia el primer ancestro que _esté posicionado_, es decir, como ya hemos dicho antes, aquel que tenga un posicionamiento no estático. Si tras ascender por el árbol buscando un ancestro posicionado, el navegador no encontrara ninguno, el elemento con posicionamiento absoluto se posicionaría con respecto al elemento `<body>`.

#### Posicionamiento fijo

Al igual que con el posicionamiento absoluto, en el posicionamiento `fixed` no se aplica el flujo normal para el elemento correspondiente y este no deja ningún hueco. Las diferencias con el posicionamiento absoluto son:

- Los desplazamientos son relativos a la ventana del documento.
    
- La caja se mantiene en esa posición de la ventana aunque el usuario se desplace arriba o abajo (_scroll_) por el documento.

![[Pasted image 20240920103355.png]]

Los espacios en blanco alrededor de los operadores son necesarios. Solo cambiando el valor inicial de la variable se consigue que se recalculen los tamaños y posiciones de todos los elementos (¡pruébalo!). Las propiedades personalizadas también se heredan, por lo que suele ser una práctica común (como en el ejemplo) declararlas para la pseudo-clase `:root` de CSS. Esta pseudo-clase selecciona el elemento raíz del árbol DOM. En HTML, este elemento es `<html>`, aunque la especificidad de `:root` es mayor. Las hojas de estilo pueden aplicarse a documentos escritos en otros lenguajes (XML, por ejemplo), por lo que `:root` es un selector más aconsejable e independiente del documento.
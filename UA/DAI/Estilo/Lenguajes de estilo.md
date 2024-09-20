## Selectores y propiedades del lenguaje CSS

### Resumen sobre selectores y propiedades de CSS

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
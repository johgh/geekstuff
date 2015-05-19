---
layout: blog
title:  "Vim: El editor incomprendido"
permalink:  "Vim-incomprendido"
date:   2015-05-02 16:30:15
category: Blog
---
![Software models](/lsi-adm3a-full-keyboard.jpg "Teclado original del ADM-3A, donde se programó Vi")

**¿Por qué alguien querría usar un editor en el que hay que pelearse solamente para empezar a escribir texto, o incluso para
salir del mismo una vez nos hemos percatado de que no es el editor que esperabamos?**

Quizás el hecho de que este editor venga instalado de serie en cualquier sistema tipo Unix le haya hecho un flaco favor:
muchos se han visto obligados a usarlo y la mayoría no guarda el mejor recuerdo de él.

Frecuentemente la potencia de este editor se confunde con falta de usabilidad, lo cierto es que si algo es comparable a
la potencia de este editor esa es su curva de aprendizaje (o [muro de aprendizaje](https://pascalprecht.github.io/2014/03/18/why-i-use-vim/#figure-1)).

## Modo normal

Nos topamos con la primera piedra en el camino. El usuario no habitual de Vim tiende a evitar el *modo normal* como si
fuera territorio comanche. Para ello memoriza únicamente 2 comandos:

* `Escape`, para salir al *modo normal*. Desde aquí únicamente ejecuta 2 comandos: `:w` para guardar y `:q` para
  salir.
* `i`, para entrar al *modo inserción*. Aquí hace uso de los cursores para desplazarse,
evitando el peligro del *modo normal*, y también toda su potencia.

Para sacar todo el partido a Vim primero deberíamos comprender su filosofía de edición. Mientras en un editor
convencional se usan los cursores, `Shift`, `Control`,
`AvPág`, `RePág`, `Inicio` y `Fin` para editar texto rápidamente, en Vim se usan las mismas teclas que utilizamos
para introducir texto. De ahí la necesidad de un modo superpuesto al *modo inserción* de texto: el *modo normal*.

El *modo normal* nos proporciona un metalenguaje mediante el cual podemos ejecutar comandos con "parámetros" (siempre a
partir de la posición actual del cursor).

Un comando del *modo normal* se corresponde con un carácter del alfabeto:

* `r` es *replace* (insert en un editor convencional)
* `i` es *insert* (cambio a *modo inserción* de texto)
* `o` es *open* (abrir una nueva línea debajo de la actual en *modo inserción*)
* `y` es *yank* (copiar en un editor convencional)
* `c` es *change* (cambiar texto, y la razón porque en Vim no se copia texto si no que se hace *yank*).

Además algunos comandos tienen "variantes" del comando original en su forma mayúscula. Entre otros:

* `I` inserta al principio de una línea
* `O` abre una línea sobre la actual
* `C` cambia texto desde donde se encuenre el cursor

El principal problema del *modo normal* visto desde los ojos de un usuario no habitual de Vim, es lo "farragoso" de tener que
cambiar entre este y el *modo inserción* todo el tiempo. Sin embargo con la práctica esto deja de ser una desventaja
para convertirse en todo lo contrario, ya que nos permite mantener las manos todo el tiempo en la posición "natural" del teclado (sin tener que
utilizar los cursores ni el ratón).

Al anterior error "conceptual" se le unen además 2 obstáculos igualmente importantes:

- La tecla `Escape`, que es la designada por defecto para el cambio al *modo normal*, se encuentra demasiado lejos para una operación
  que debemos realizar constantemente (si te preguntas porque se eligió esta tecla, echa un vistazo a la imagen del
  teclado que hay debajo del título). La solución a este problema es evitar su uso utilizando `Control`+`c` u otra tecla configurada a tal
  efecto.

- El desconocimiento por parte del usuario inexperto de los comandos que nos facilitan el retorno al modo inserción:

>
* `i`: entra al *modo inserción* en la posición actual
* `a`: entra al *modo inserción* en la siguiente posición a la que nos encontrabamos
* `s`: entra al *modo inserción* sustituyendo el carácter actual
* `I`: entra al *modo inserción* en el primer carácter de la línea
* `A`: entra al *modo inserción* en el último carácter de la línea
* `o`: entra al *modo inserción* después de insertar una nueva línea debajo de la actual
* `O`: entra al *modo inserción* después de insertar una nueva línea encima de la actual
* `cc`: entra al *modo inserción* borrando toda la línea actual
* `C`: entra al *modo inserción* desde el carácter actual borrando todo lo que quede en la línea

Finalmente, como decía al principio, ciertos comandos requieren de parámetros para ser ejecutados. Es lo que se conoce como *operator pending
mode*. De ahí que no hablemos de atajos (como en cualquier editor convencional),
sino de comandos (o *operadores*, según el manual de Vim) que pueden realizar diferentes acciones según los parámetros utilizados.

>
Comandos que hacen uso de parámetros (*operator pending mode*)
: `y`, `d`, `c`, `f`(find)

>
Comandos sin parámetros
: `u` (undo), `x`, `s`, `p`/`P` (pegar/pegar antes del cursor), `o`/`O`, `i`/`I`, `a`/`A`

Las 2 clases de comandos que vemos arriba soportan además un número (o *counter*), que especifica el número de veces que se debe ejecutar el
comando. Los comandos con parámetros aceptan al menos 1 parámetro que corresponda bien a un `motion` o a un `text
object`. Para más información sobre el formato de estos parámetros ver [aquí](/vim/#tocAnchor-1-1).

Sintáxis de un comando del modo normal
: `counter` + `comando` + [`text object` / `motion`] + [\<parámetro adicional\>]

## El factor repetición

Pero para entender realmente la potencia del *modo normal*, debemos tener en cuenta el factor repetición. Cualquier
cambio realizado en el *modo inserción* queda guardado automáticamente y listo para ser repetido mediante el comando `.`

Además la granularidad de
los cambios en Vim (uno puede cambiar una letra con `s`, 2 [*palabras*](/vim/#standard-vim-words) con
`2cw`o todo lo que aparezca hasta una determinada palabra con `c/palabra`) permiten la repetición de estos mediante el
citado comando `.` o mediante la creación de macros y otros comandos que no serían posibles en un editor convencional
(en ocasiones se puede suplir con el uso de un diálogo de búsqueda y reemplazo)

## El portapapeles

Otro gran desconocido para el usuario no habitual de Vim suele ser el uso del - o más bien *los* - portapapeles. El
desconocimiento de que comandos copian texto al portapapeles es objeto de frustración en el momento de recuperar texto
de éste, ya que el texto que habíamos copiado cuidosamente mediante el comando *yank* parece haber desaparecido misteriosamente.
Concretamente, estos son los comandos que copian texto al portapapeles:

>
* `y`: sólo copia texto. Registros afectados: registro `0` y registro por defecto (`"`)
* `d`: borra texto (y copia). Registros afectados: registro `1`/`-` y registro por defecto (`"`)
* `c`: cambia texto (y copia). Registros afectados: registro `1`/`-` y registro por defecto (`"`)
* `x`: borra carácter (y copia). Registros afectados: registro `1`/`-` y registro por defecto (`"`)
* `s`: sustituye carácter (y copia). Registros afectados: registro `1`/`-` y registro por defecto (`"`)

A la hora de recuper texto del portapapeles mediante el comando `p`/`P` debemos tener en cuenta que estos comandos
recuperan el texto almacenado en el registro por defecto (`"`). Por tanto si queremos recuperar el texto
que hemos copiado mediante *yank* tendremos 2 opciones dependiendo del modo en que nos encontremos:

* Desde el *modo inserción*: `Control`+`r` seguido del símbolo de nuestro registro (en este caso `0`)
* Desde el *modo normal*: usando el comando `"0p`/`"0P`

Un poco más [abajo](/Vim-incomprendido/#personalizando-vim) podemos ver algunas maneras de hacer más
accesible la gestión del portapapeles.

Particularmente interesante es integrar el portapapeles de Vim con el del sistema, utilizando el registro *unnamed plus*
(`"+`) como registro por defecto. Este registro engloba tanto al registro por defecto de Vim (`""`) como el portapapeles de
nuestro sistema operativo (`"*`)

## La práctica
Ciertamente la potencia de edición de Vim puede aturdir al principio, la misma cosa se puede hacer de muchas maneras,
pero ¿cual es la mejor manera?

Está claro que ni utilizar el [menor número de pulsaciones](http://www.vimgolf.com/) en cada momento, ni usar Vim de la forma más
"perezosa" posible (como si se tratara de un editor convencional) debe ser nuestro objetivo. La
[práctica](https://pragprog.com/book/dnvim/practical-vim) será nuestra mejor
consejera, y en poco tiempo comenzaremos a memorizar algunas secuencias de teclas recurrentes. He aquí algunos ejemplos:

Cambiar palabra (sin espacio posterior)
: `c[i]w`

> La *i* (inner) será necesaria siempre que no nos encontremos a principio de palabra y queramos cambiar la palabra entera

Borrar palabra y espacio posterior
: `d[a]w`

> La *a* será necesaria siempre que no nos encontremos a principio de palabra y queramos cambiar la palabra entera y el
espacio (usar i si no queremos borrar el espacio) Ver [text objects](/vim/#tocAnchor-1-1-3) para saber más

Cambiar el valor de un string delimitado por '
: `ci'`

Duplicar un párrafo y posicionarse al principio del segundo
: `yap` + `gP`

Reemplazar el argumento de una función de C con lo que tengamos en el portapapeles
: `vt,` + `p`

¿Pero cómo se puede pensar en lo que se está escribiendo al mismo tiempo que
se piensa en el comando que conviene ejecutar en el momento?

La respuesta es que no se puede. Aprender Vim como cualquier cosa requiere
tiempo y dedicación. Si somos persistentes pronto nos daremos cuenta de que comenzamos a utilizar comandos sin
pensar en lo que estamos haciendo. Ese es precisamente el objetivo, que la memoria muscular haga el trabajo por nosotros
para que sólo tengamos que pensar en lo que queremos escribir.

## Personalizando Vim

Vim fue diseñado con el objetivo de ser extremadamente potente y flexible. Y eso es bueno, pero tiene un precio que a
veces nos gustaría evitar pagar: complejidad.

A medida que interiorizamos los comandos de Vim nos damos cuenta que repetimos determinadas acciones todo el tiempo, que
nos hacen perder tiempo, o incluso peor, nos desconcentran levemente de nuestra labor. Es el momento de dejar de
adaptarnos a Vim y comenzar a adaptar el editor a nuestras necesidades y preferencias.

He aquí algunas de [mis personalizaciones](https://github.com/johgh/vim), que quizás puedan ser de inspiración para
solucionar algunos "problemas" comunes. El código incluído se debe añadir al fichero *.vimrc*

Añadir línea y salir salir del *modo inserción* (tanto desde el *modo inserción* como desde del *modo normal*)
: {% highlight vim %}
    nnoremap <A-o> o<esc>
    nnoremap <A-O> O<esc>
    inoremap <A-o> <esc>o<esc>
    inoremap <A-O> <esc>O<esc>
{% endhighlight %}

Permitir pegar múltiples veces lo mismo después de pegar desde *modo visual*
: {% highlight vim %}
        vnoremap p pgvy
{% endhighlight %}

No copiar al portapapeles texto sobre el que se ejecuta comando change
: {% highlight vim %}
    nnoremap c "_c
    nnoremap C "_C
{% endhighlight %}

Usar registro unnamedplus como portapapeles por defecto
: {% highlight vim %}
        set clipboard=unnamedplus
{% endhighlight %}

> Integración del portapapeles de Vim con el del sistema.
        
Permitir el uso del atajo `Control`+`v` para pegar en *modo inserción*/comando
: {% highlight vim %}
    inoremap <C-v> <C-r>+
    cnoremap <C-v> <C-r>+
{% endhighlight %}

Alternar entre registro por defecto y auxiliar (@p)
: {% highlight vim %}
    nnoremap <F11> :let @h=@+ \| let @+=@p \| let @p=@h <CR>
{% endhighlight %}

> De esta forma podemos dejar guardado en un registro auxiliar lo que tenemos en el portapapeles, y trabajar siempre con
el registro principal con los comandos `y` y `p`, cuando hemos terminado volver a recuperar lo que teníamos
anteriormente en el portapapeles

Facilita la adición (append) de texto al portapapeles
: {% highlight vim %}
    nnoremap <silent> gy :let @h=@+<CR>"Hyy:let @+=@h<CR>
    vnoremap <silent> gy :normal gy<CR>
{% endhighlight %}

> utilizamos yy para copiar la primera línea,  gy desde el *modo normal* o *visual* para añadir una línea o varias y p para
pegar finalmente el texto. (la forma estándar sería: "ayy -> "Ayy -> "ap)

Permitir el uso de macros y del comando . sobre una selección visual
: {% highlight vim %}
    vnoremap @@ :normal @@<CR>
    vnoremap @a :normal @a<CR>
    vnoremap . :normal .<CR>
{% endhighlight %}
    
Búsqueda literal, deshabilitando expresiones regulares
: {% highlight vim %}
    nnoremap / /\V
{% endhighlight %}
    
Cerrar *buffer* pero no salir de Vim
: {% highlight vim %}
    map <silent> <leader>q :only<CR>:bd<CR>
{% endhighlight %}
    
Ir al *buffer* visitado anteriormente
: {% highlight vim %}
    nmap <leader><space> :b#<CR>
{% endhighlight %}

Cerrar quicklist y limpiar
: {% highlight vim %}
    map <Leader>Z :cex []<CR>:ccl<CR>
{% endhighlight %}

Guardar con `Control`+`s` desde cualquier modo y salir a *modo normal*
: {% highlight vim %}
    map <C-s> :w<CR>
    vmap <C-s> <esc>:w<CR>gv
    inoremap <C-s> <esc>:w<CR>
{% endhighlight %}
    
Permitir guardar fichero mediante *sudo*
: {% highlight vim %}
    cmap w!! w !sudo tee % >/dev/null
{% endhighlight %}

Subir y bajar rápidamente presionando `Control`
: {% highlight vim %}
    map <C-j> 4j
    map <C-k> 4k
{% endhighlight %}

Navegar en el mode comando con `Control`+`n`/`p` en lugar de con los cursores
: {% highlight vim %}
    cnoremap <C-n> <down>
    cnoremap <C-p> <up>
{% endhighlight %}

### Vim como *IDE*

Una vez dominados los [comandos de gestión de ficheros](/vim/#tocAnchor-1-21) que proporciona Vim por defecto (así como el
concepto de *buffer* y *ventana*), si realmente queremos utilizar Vim como nuestro *IDE* es posible que echemos en falta un buscador de
ficheros y un árbol de directorios. Además querremos de alguna forma poder realizar acciones por proyecto (como buscar
un texto por ejemplo)... en este caso la solución viene de la mano de plugins.

* [Vim-rooter](https://github.com/airblade/vim-rooter): sitúa el path del *buffer* actual en el la raíz del proyecto del mismo
* [NERDTree](https://github.com/scrooloose/nerdtree): árbol de directorios
* [CtrlP](https://github.com/ctrlpvim/ctrlp.vim): permite buscar ficheros dentro de un proyecto así como los últimos *buffers* abiertos y los *buffers* actuales
* [Ag](https://github.com/rking/ag.vim): grep más rápido, permite excepciones dentro del proyecto e incluye atajos
  útiles para *quicklist*
* [Tagbar](https://github.com/majutsushi/tagbar): vista de *outline* de nuestras clases

En ocasiones necesitaremos el path donde se encuentra nuestro fichero, en mi caso escribo simplemente `~~` haciendo uso del mecanismo de expansión de
Vim. También puede ser útil especificar un directorio de inicio por defecto:

Expansión de rutas en *modo comando*
: {% highlight vim %}
    cnoremap <expr> ~~ getcmdtype() == ':' ? expand('%:h').'/' : '~~'
    cnoremap <expr> ~ getcmdtype() == ':' ? expand('~').'/' : '~'
{% endhighlight %}
    
Directorio de inicio por defecto
: {% highlight vim %}
    if !empty(glob("$HOME/workspace/"))
    cd $HOME/workspace/
    endif
{% endhighlight %}
    
## Más allá del *modo normal*

A continuación se listan algunas de las características más interesantes que no se suelen encontrar en otros editores o
entornos de programación:

* Posibilidad de navegación por donde hemos pasado (`:jumps`) y por donde hemos realizado cambios (`:changes`)
* Creación de macros (incluyendo los comandos de cualquier modo) y la posibilidad de edición de las mismas
* [*Modo comando*](/vim/#tocAnchor-1-13) que permite la ejecución de comandos sobre rangos de líneas o sobre múltiples rangos mediante el comando
  global
* Repetición de búsquedas, [comandos](/vim/#tocAnchor-1-13-4), macros y cambios realizados en el *modo normal* sobre cualquier *buffer*
* La inclusión de los "comandos" del *modo normal* dentro del comando :normal
* *Modo visual* (`v`/`V`) y *submodos de bloque* (`Control`+`v`) que permiten la ejecución de ciertos comandos de una forma más intuitiva para el usuario
* Árbol de cambios que permite deshacer y rehacer cambios que se pierden en editores convencionales (para ver árbol
  gráficamente es necesario es uso del plugin [gundo](https://github.com/sjl/gundo.vim))
* Uso de múltiples portapapeles
* Personalización total del editor mediante la configuración, el lenguaje Vimscript y plugins

## Preguntas y respuestas

**¿De verdad merece la pena invertir nuestro tiempo en aprender a utilizar un editor de texto?**

No hay una respuesta simple a esa pregunta, Vim no es para todo el mundo, cada cual debe valorar que le aporta el uso
del editor. Eso sí, si damos el paso es vital dedicarle el tiempo suficente para que sea la memoria muscular, y no
nuestra cabeza, la que tome el control.

**¿Quién mantiene Vim?**

Vim es software libre. El desarrollo ha sido llevado a cabo casi exclusivamente por un desarrollador
desde 1991, y tratando de ser retrocompatible con el editor Vi originalmente escrito en 1976, ha heredado algunos
ajustes por defecto poco afortunados, que hacen que sea casi obligatorio configurarlo inicialmente a [nuestra
medida](/Vim config/).

**¿Cuál será el futuro del editor?**

Aunque un editor que se mantiene activo desde hace más de 40 años, tiene que tener una fuerte comunidad
detrás, son incluso más importantes los conceptos que subyacen del mismo. Así como Vim reemplazó al Vi original no
sería de extrañar que [otro editor](http://neovim.io/) pudiera reemplazar al actual y continuar así con su
[legado](https://medium.com/@mkozlows/why-atom-cant-replace-vim-433852f4b4d1).

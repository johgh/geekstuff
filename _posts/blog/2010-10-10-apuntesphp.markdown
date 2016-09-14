---
layout: blog
title:  "PHP. Apuntes"
permalink:  "apuntesphp"
date:   2014-03-23 00:00:01
category: Blog
tags: Web
---
# "Construcciones del lenguaje" y comparación de tipos

- `isset` y `empty` son construcciones del lenguaje. A diferencia de cualquier otra función, estas construcciones no lanzan error en tiempo de ejecución si la variable pasada como parámetro no existe.

    El propósito de estas funciones debe ser exclusivamente la comprobación de la existencia de variables que puedan no haber sido declaradas (por ejemplo parámetros del usuario `$_GET`). Es recomendable la inicialización de variables para evitar el uso de estas construcciones dentro de lo posible.

- En PHP una variable no definida tiene valor `NULL` (único valor posible del tipo de datos `NULL`), por tanto no se puede distinguir entre una variable no existente y una a la que se le haya asignado valor nulo. `isset` devolverá falso para los dos casos. No se lanzará error al utilizar una variable a la que se ha asignado `NULL` previamente (pero si habrá error si se ha hecho `unset` de la variable).

- La construcción `empty` equivale a `!isset($var) || $var == false`. `if (!empty($var))` es útil cuando esperamos un valor pero no sabemos si la variable existe. Si la variable debe existir usaremos simplemente `if($var)`, de lo contrario no veríamos el error en tiempo de ejecución de no existir la variable.

- PHP por defecto evalúa las expresiones de forma no estricta. Por ejemplo `if('entra')` se evalúa como cierto. Si queremos que la expresión anterior no se evalúe como cierta deberemos especificar la condición de forma estricta: `if ('entra' === true)`

- No se debe usar la construcción `empty` para detectar cadenas vacías puesto que la cadena `"0"` sería considerada vacía debido a la comparación no estricta `== false` que utiliza `empty`. Para detectar cadenas vacías necesitaremos 2 condiciones: `(!isset($mystring) || $mystring == null)`

> mientras que `"0" == false` se evalua como cierto, `"0" == null` retorna falso. Para más información ver [tabla de comparaciones no estrictas](http://php.net/manual/en/types.comparisons.php)

- Para conocer el tipo de una variable deberemos usar las siguientes funciones: `is_float`, `is_int`, `is_array`, `is_null`, `is_bool`, `is_object`, `is_string`


<br />

---
<br />


# Excepciones y mecanismo de control de errores

- En PHP se pueden encontrar 3 tipos de errores en tiempo de ejecución que en algunos casos podemos necesitar controlar:

1. "Errores lógicos”, que podemos detectar, por ejemplo, mediante el testeo del retorno de una función
2. Errores en servicios de red (posiblemente errores fatales)
3. Otros errores fatales que detienen la ejecución del programa (a diferencia de java, php no lanza Excepciones automáticamente en ningún caso, únicamente errores fatales)

- El uso de Excepciones no previene en ningún caso el mecanismo de control de errores según se encuentre configurado en `php.ini`

- Si se quiere lanzar una excepción relacionada con algún método que hace uso del mecanismo de control de errores de php (por ejemplo, en el caso que devuelva un warning), deberemos utilizar `@` para suprimir el mensaje propio de php:

{% highlight php startinline %}
$sp = @fsockopen('192.168.1.66', 5000, &$errorno, &$errorstr);
if (!$sp)
    throw new fSockException('Error fsockopen');
{% endhighlight %}

- Es posible pasar un objeto de cualquier tipo a la cláusula `throw` (por ejemplo si necesitamos debugar un objeto problemático), sin embargo lo más habitual es utilizar un objeto de la clase Exception o una clase derivada de esta misma clase.

- Para definir una excepción del usuario será necesaria la creación de una clase que extienda de Exception.

- El uso de un objeto de tipo Exception utilizado en un bloque `catch` permite la captura de excepciones genéricas. Sin embargo, es recomendable el uso de excepciones definidas por el usuario sobre cada tipo de excepción que esperamos, haciendo posible capturarlas en su correspondiente `catch`:

{% highlight php startinline %}
catch (fSockException $e) { /* handle exception */ }
{% endhighlight %}

- Los métodos definidos en `Exception` son finales, de forma que en las excepciones definidas por el usuario únicamente podemos añadir nuevos métodos, no redefinirlos (también es posible dejar la clase vacía)

- Sin embargo si podemos hacer <i>override</i> del método mágico `__toString` (que es lanzado al utilizar el objeto como una cadena), para modificar el aspecto visual de la excepción, y luego printar $myException mediante `echo`

- Por otro lado, las excepciones no son la única manera de tratar con errores controlados. La función `trigger_error()` lanzará un error, warning, etc. (dependiendo de la constante que pasemos en el segundo parámetro) que será tratado de la misma forma que cualquier otro error propio de PHP (built-in).

- Si utilizamos el método `set_error_handle('myErrorHandler')` este lanzará el método que le pasemos como parámetro cuando se produzcan errores de usuario, warnings y notices. De esta forma podremos cambiar el aspecto del error propio de PHP o incluso permitir que el script continúe su ejecución (siempre que no se finalize mediante `exit`).

- Algunos errores fatales de PHP no llaman en ningún caso al controlador de errores definido por el usuario (por lo que si no se quiere que ocurran deberán ser controlados mediante lógica adicional).

- En el caso de retornar falso en el controlador de errores definido por el usuario, el controlador de errores propio de PHP será lanzado. De esta forma se pueden controlar únicamente los errores lanzados mediante `trigger_error()`, dejando directamente a PHP que se encargue de mostrar el resto de errores.

<br />


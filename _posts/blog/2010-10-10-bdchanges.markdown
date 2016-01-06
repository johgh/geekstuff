---
layout: blog
title:  "Control de cambios de BD"
permalink:  "bdchanges"
date:   2015-10-01 00:00:01
category: Blog
tags: Web
---
La naturaleza del código de BD no es la misma que la de cualquier otro código:

- Para realizar cambios solo podemos hacerlo mediante la ejecución de scripts de cambios, no basta con modificar el código
- No podemos aplicar cualquier tipo de cambio (sin perder datos, se entiende)

Por ello, no es suficiente un sistema de control de versiones tradicional para mantener un control de los cambios en BD.

# Proceso de actualización automatizado
- Inicialmente podemos crear un solo fichero de cambios para cada release
- Al principio del script se inserta un registro en la tabla <schema>changeLogDB con:

    {% highlight bash %}
        id | version (XX.XX.XX) | file | execution_date
    {% endhighlight %}

- Para actualizar la base de datos deberemos ejecutar un script upgrade.sh:

    {% highlight bash %}
        $ upgradeDB.sh <schema> <version_hasta_donde_actualizar>
    {% endhighlight %}

Este script ejecuta las actualizaciones que no se encuentran registradas en la base de datos destino, de forma secuencial. Si el fichero de actualización con el id más pequeño no es consecutivo al registro con el id más grande, la BD no podrá ser actualizada.

# Un fichero por objeto
- Por cada objeto creamos un fichero. Cada objeto debe comprobar inicialmente si ya existe (para ser borrado) y finalmente asignar sus permisos. (Otra posibilidad es crear un fichero por cada grupo de cambios relacionados)

- Cada fichero debe tener como prefijo el orden en el que debe ser ejecutado (prioridad).

Si ocurre un error al ejecutar las actualizaciones sabremos exactamente qué codigo ha fallado al mirar el último registro de la tabla <schema>changeLogDB.

# Subida a producción

Nuestro objetivo es asegurarnos de que los cambios realizados en desarrollo quedan guardados correctamente en un fichero/s de cambios para ser ejecutados en PRODUCCIÓN sin problemas. Para ello:

1. Obtenemos los cambios entre desarrollo y PRODUCCIÓN.

2. Generamos nuestros ficheros de cambio con el insert de nuestro cambio a <schema>changeLogDB en el inicio de cada fichero.

3. Ejecutamos upgradeDB.sh <schema> en entorno de PREPRODUCCION (copia de nuestro entorno de desarrollo antes de aplicar ningun cambio de BD) para comprobar que el script funciona correctamente

3. Si todo ha ido bien, sabemos que el script no fallará en el entorno de PRODUCCIÓN

4. Cabe la posibilidad de que nos hayamos dejado cambios a aplicar, así que siempre deberíamos hacer un testeo general apuntando al entorno de PREPRODUCCION antes de subir finalmente a PRODUCCIÓN

5. Si todo está bien, ejecutamos upgradeDB.sh <schema> en el entorno de PRODUCCIÓN

# Enlaces de interés

- [http://c2.com/cgi/wiki?DatabaseBestPractices](http://c2.com/cgi/wiki?DatabaseBestPractices)
- [http://thedailywtf.com/articles/Database-Changes-Done-Right](http://thedailywtf.com/articles/Database-Changes-Done-Right)


## Preparar sublime text para acceder a los ficheros de nuestra web en AWS
1. Descargar la llave .ppk desde nuestra consola de bitnami (servidor > manage > connect)

## Arrastrar a sublime text los ficheros que necesitamos para nuestra nueva web.
1. Arrastramos la carpeta templates hasta sublime text  C:/bitnami/processwire/apps/processwire/htdocs/site/templates   

## Preparamos la cabecera y pie compartido en todas las páginas
1. Borramos el contenido de _init.php, _main.php y home.php   
2. Vamos a instalar una plantilla, para ello abrimos en sublime text cualquier html de la plantilla.  
3. Copiamos en _init.php la parte de la cabecera que compartiran todas las páginas de nuestra web. Si abrimos el inspector veremos muchas lineas en rojo, pues no encuentra los ficheros css, volveremos sobre este aspecto luego.
4. Copiamos la parte del pie que se repetirá en todas las páginas en _main.php


## Instalar todos los ficheros CSS y JS necesarios para esta plantilla
1. Arrastramos todos los css a nuestra carpeta de styles y los js a scripts ( por SFTP hacer upload folder)
2. Hacer lo mismo con font e images.
3. Ahora en todas las lineas, tanto de css como de js sustituiremos de la siguiente forma

```php
    donde ponga por ejemplo: css/bootstrap.min.css  =>  
    <?php echo $config->urls->templates?>css/bootstrap.min.css  
    
```

## Logo y fuentes
1. Si tenemos un logo o fuentes debemos seguir los mismos pasos que en el caso de css y js  


## Imágenes  
Actuaremos del mismo modo con las imágenes, tanto en el header como en cada página hay que cambiar la ruta:  

```php
    
    <img class="img-responsive img-circle" src="<?php echo $config->urls->templates?>images/testimonials1.png">
    
```

## Páginas
Ahora podemos ya empezar a crear cada página de nuestra web.  
La página principal es home.php (inicio, portada)  

Para que vaya al home también hay que cambiar la ruta en el header:  
```php
<li><a href="<?php echo $config->urls->root?>">Home</a></li>
<li><a href="<?php echo $config->urls->root?>nosotros/">About Us</a></li>
<li><a href="<?php echo $config->urls->root?>servicios">Servicios</a></li>
<li><a href="<?php echo $config->urls->root?>portfolio">Portfolio</a></li>
```

## Cambiar el idioma [video](https://youtu.be/lWXvyRH2tpw)
1. En el menú principal: Modules > Core y activar "Languages Support"
2. Ahora desde el menu principal ir a Setup y Languages, add new
3. Tanto en title como name poner **es**
4. En la nueva ventana que se ha abierto, pulsar el texto rojo a mitad de pantalla "language packs"
5. Pinchar en Spanish(es-ES) v.2 y al final de la página darle a "Download this module"
6. Arrastramos el fichero descargado a  Site Translation Files y en pocos segundo podemos pinchar en Save
7. Ahora necesitamos decirle que nuestro idioma preferido es el español
8. Vamos al menu Access > users y pinchamos en el nuestro
9. Al final seleccionamos **es** y ya tenemos el idioma preferido.

## Instalar angular
1. Necesitamos instalar el módulo Pages2JSON
2. Crear carpeta PwAngular en C:/bitnami/processwire/apps/processwire/htdocs/site/modules
3. Poner el contenido de https://github.com/manviny/processgular/tree/master

 ## Vamos a probarlo en home.php
 ```php
 
    ## Pegar este código
<script>
    app.controller('HomeCtrl', function ($scope, PW) {

     	$scope.saluda = function(){
     		toastr.info( 'Bienvenido '  ,{timeOut:4000});
     	}

    });
</script>

<div class="container" ng-controller="HomeCtrl">
	<button ng-click="saluda()">saluda</button>
</div>
 ```


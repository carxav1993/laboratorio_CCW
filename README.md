# LABORATORIO - COMPUTACIÓN EN EL CLIENTE WEB

## Estudiante: Carlos Vega Oyola

![](https://i1.rgstatic.net/ii/profile.image/AS%3A526183737839616%401502463387127_xl/Carlos_Vega_Oyola.png)

El presente informe es una actividad denominada **Laboratorio:  Creación de una aplicación web en el cliente** de la asignatura **Computación en el Cliente Web** del ***Máster Universitario de Ingeniería del Software y Sistemas Informáticos***, en donde se detalla el uso del Framework jQuery a lo largo de los años y como ha ido evolucionando para una mejor codificación y ahorro de tiempo al momento de efectuar la programación del mismo. 

Como ejemplo de ilustración se realizarán peticiones AJAX[^ajax], como normalmente se implementan con javascript[^javascript] nativo y con jQuery[^jquery] de forma escalonada ante las mejoras que ha sufrido positivamente durante los años, para obtener chistes acerca de [Carlos Ray Norris](https://chucknorris.com/) (Chuck Norris) y además como se realizan actualmente. El sitio web que contiene los chistes acerca de Chuck Norris se denomina [The Internet Chuck Norris DataBase](http://www.icndb.com) y en su apartado [Api](http://www.icndb.com/api/) se muestra como acceder a dicha información.

Para la realización de este laboratorio se utilizarán:

- **Editor**: Visual Studio Code, para realizar la instalación y conocer como funciona recomiendo el siguiente [enlace](https://code.visualstudio.com/docs) en donde se encontrará toda la información necesaria.

![Visual Studio Code](http://voidcanvas.com/wp-content/uploads/2017/09/Visual-Studio-Code-For-Windows.jpg)

- **Framework Front-end**: Materialize CSS utilizado para representar los datos que se va a consumir mediante el api de los chistes, el sitio oficial de este framework se encontrará en el siguiente [enlace](http://materializecss.com/). 
![Materialize CSS](http://cdn.vibidsoft.com/blog_image/2016/08/meterialize.jpg)

> **Importante**
>  
> - Para la utilización del Framework Front-end **Materialize CSS**, se utilizará el CDN como se indica en su sitio web oficial, para más información dejo este [enlace](http://materializecss.com/getting-started.html).
> - Cabe mencionar que el Framework posee diferentes componentes CSS y documentación para implementarlos en una página web, dentro de esta actividad se utilizará un [slider](http://materializecss.com/media.html) donde se presentarán imágenes de Chuck Norris y como descripción el chiste que se obtiene a través del AJAX. 
> - A continuación, en el siguiente fragmento de código, se muestra como vincular los archivos css y javascript del Framework CSS en la cabecera del html.

```
<!-- CDN CSS del Framework Front-end Materialize CSS-->
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/0.100.2/css/materialize.min.css">

	<!-- Compiled and minified JavaScript -->
	<!-- CDN JS del Framework Front-end Materialize JS-->
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/0.100.2/js/materialize.min.js"></script>
```
Además de los dos enlaces CND, se debe incluir el enlace de jQuery para que puedan funcionar los componentes de Materialize CSS.


### Comienzo del laboratorio

#### <i class="icon-file"></i> Ajax mediante Javascript nativo

1. Para el inicio de este laboratorio, se creará un archivo html denominado *1_javascript_ajax.html*.
2. Luego se añade en la cabecera de la página el enlace del archivo css y js respectivamente del Framework mediante CDN.
3. Se usa ***XMLHttpRequest*** entre las etiquetas `<javascript type="text/javascript"></javascript>` para realizar la petición AJAX y obtener el resultado esperado, el código utilizado se observa a continuación.


```
xmlhttp = new XMLHttpRequest();
xmlhttp.open('GET', 'http://api.icndb.com/jokes/random/5', true);
xmlhttp.onreadystatechange = function(){
	var textoChiste = JSON.parse(this.response).value;
	console.log('chistes recibido: ' + textoChiste.length);
	var contenedor = document.getElementsByClassName("slides");
	for (var i = 0; i < textoChiste.length; i++) {
	document.getElementById("image"+i).removeAttribute('src');
	document.getElementById("image"+i).setAttribute('src',arrayImagenes[i]);
	document.getElementById("chiste"+i).innerHTML = textoChiste[i].joke;
	console.log(textoChiste[i].joke);
	}			
}
xmlhttp.send();
```

El código de esta página se observa en el siguiente [enlace](https://github.com/carxav1993/laboratorio_CCW/blob/master/1_javascript_ajax.html). El resultado del mismo se muestra en el siguiente [enlace](http://investigacion.utmachala.edu.ec/laboratorio_CCW/1_javascript_ajax.html).

> Para complementar el código javascript nativo implementado para efectuar el primer apartado, sirvió de apoyo la página de la [W3School - Js](https://www.w3schools.com/js/).

___

#### <i class="icon-pencil"></i> Ajax mediante jQuery (2006)

1. Para este apartado, se creará un archivo html denominado *2_jquery_ajax.html*.
2. Luego se añade en la cabecera de la página el enlace del archivo css y js respectivamente del Framework mediante CDN.
3. Se usa `$.ajax(...)` entre las etiquetas `<javascript type="text/javascript"></javascript>` para realizar la petición AJAX y obtener el resultado esperado, el código utilizado se observa a continuación.

```
$.get("http://api.icndb.com/jokes/random/5", (response) => {
	var textoChiste = response.value;
	console.log(textoChiste.length);
	for (var i = 0; i <= textoChiste.length - 1; i++) {
		$("#image"+i).removeAttr("src");
		$("#image"+i).attr('src', arrayImagenes[i]);
		$("#chiste"+i).html(textoChiste[i].joke);
	}
});
```
El resultado es el mismo, solo que en código se puede observar notablemente la reducción de este mediante el uso de jQuery a través de este [enlace](https://github.com/carxav1993/laboratorio_CCW/blob/master/2_jquery_ajax.html), además del resultado de este apartado se muestra en el siguiente [enlace](http://investigacion.utmachala.edu.ec/laboratorio_CCW/2_jquery_ajax.html).

> Para complementar el código jQuery implementado para efectuar este apartado, sirvió de apoyo el sitio oficial de jQuery, específicamente la manipulación del [DOM](http://api.jquery.com/category/manipulation/).

___

#### <i class="icon-pencil"></i> Ajax mediante el plugin jQuery a partir del 2014

1. Para este apartado, se creará un archivo html denominado *3_jquery_plugin_ajax.html*.
2. Luego se añade en la cabecera de la página el enlace del archivo css y js respectivamente del Framework mediante CDN.
3. Ahora se utilizará el plugin de jQuery que han incluido la página de chistes los respectivos datos, el mismo se encuentra en el siguiente [enlace](http://www.icndb.com/libraries/javascript-jquery-plugin/). Cabe recordar que para utilizar este plugin se debe ubicar en la cabecera del documento html encerrado entre las etiquetas en el atributo src `<script src="http://_enlace_"></script>`, el enlace de donde se obtendrá la información, en este caso es http://code.icndb.com/jquery.icndb.min.js.
4. Para la obtención de la información la página ofrece métodos para la obtención de información, el que se va a tomar es `$.icndb.getRandomJokes()`, que trae un número indicado de chistes.

```
$.icndb.getRandomJokes({
	number: 5,
    success: (response) => {
	    response.forEach(element => {  
	        var indice = response.indexOf(element); 
            $( "#image"+indice ).removeAttr('src'); 
            $( "#image"+indice ).attr('src', arrayImagenes[indice]); 
            $( "#chiste"+indice ).html(element.joke); 
         });
    }
});
```
El resultado es el mismo, solo que en código se puede observar notablemente la reducción de este mediante el uso del plugin jQuery como se observa en este [enlace](https://github.com/carxav1993/laboratorio_CCW/blob/master/3_jquery_plugin_ajax.html), y resultado en el siguiente [enlace](http://investigacion.utmachala.edu.ec/laboratorio_CCW/3_jquery_plugin_ajax.html).

> Para complementar el código jQuery implementado para efectuar este apartado, sirvió de apoyo el sitio oficial de jQuery, específicamente la manipulación del [DOM](http://api.jquery.com/category/manipulation/).

_____

#### <i class="icon-cog"></i> Web Components (presente)

1. Para este apartado, se creará un archivo html denominado *4_web_components.html*.
2. Luego se añade en la cabecera de la página el enlace del archivo css y js respectivamente del Framework Front-end mediante CDN.
3. Posteriormente se añade en la cabecera del documento HTML una etiqueta `<link>` y en el atributo ***rel*** se escribe ***"import"*** además del ***href*** que debe estar vinculado el enlace donde se tomará referencia el web component, quedando de la siguiente manera: `<link rel="import" href="https://raw.githubusercontent.com/erikringsmuth/chuck-norris-joke/master/chuck-norris-joke.html">`.
4. Para la obtención de la información únicamente se debe indicar las etiquetas `<chuck-norris-joke></chuck-norris-joke>`.

El resultado es el mismo, aunque en código queda muy simplificado a una única linea de etiqueta del html, como se muestra en el siguiente [enlace](https://github.com/carxav1993/laboratorio_CCW/blob/master/4_web_components.html) y resultado en el navegador en este [enlace](http://investigacion.utmachala.edu.ec/laboratorio_CCW/4_web_components.html).

> Mayor información de los web components, sírvase revisar el siguiente [enlace](https://www.webcomponents.org/).

----
> Se recomienda revisar el sitio web [StackEdit.io](https://stackedit.io) para aplicar sintaxis avanzadas sobre creación de documentos "markdown", además de revisar el sitio web [MarkDown](https://markdown.es/sintaxis-markdown/).

### Estadísticas (Aporte propio)

He considerado agregarle un plus a esta actividad, es sobre la verificación del rendimiento al momento de cargar la página en los navegadores populares, es decir, cuántos segundos tardan y número de peticiones que realizan con el objetivo de verificar si es que jQuery reduce el rendimiento de manipulación.

#### Documento 1 **(*1_javascript_ajax.html*): **

Navegador| Segundos | Peticiones
-------- | :-------:| :--------:
Mozilla Firefox | 3.01 | 17
Google Chrome | 2.14 | 21

#### Documento 2 ***(2_jquery_ajax.html)***: 
Navegador| Segundos | Peticiones
-------- | :-------:|:--------:
Mozilla Firefox | 3.13 | 17
Google Chrome | 2.81 | 21

#### Documento 3 ***(3_jquery_plugin_ajax.html*)**:
 
Navegador| Segundos | Peticiones
-------- | :-------:|:--------:
Mozilla Firefox | 5.07 | 17
Google Chrome | 3.95 | 21

#### Documento 4 **(*4_web_components.html*)**:
 
Navegador| Segundos | Peticiones
-------- | :-------:|:--------:
Mozilla Firefox | 6.55 | 17
Google Chrome | 6.30 | 21

> **Conclusión** Ante estos resultados (fue la primera que se tomó al momento de recargar la página usando la herramienta para desarrolladores que ofrecen los navegadores Google Chrome y Mozilla Firefox) se puede llegar a concluir que si bien es cierto jQuery facilita mucho en realizar múltiples acciones al momento de manipular el DOM que javascript nativo, pero nos cuesta un poco de rendimiento al momento de completar las peticiones, aunque sea mínimo y poco perceptible, lo es.
> Efectúe este análisis porqué en el foro que tenemos de la asignatura se había comentado acerca del rendimiento que penaliza el uso de jQuery. 
> Sin embargo, jQuery hoy es día es uno de los Framework más usado a nivel mundial, solucionando un sinnúmero de inconvenientes y logrando efectuar muchas acciones con pocas líneas de código, por ello está correcto su lema "Write less, do more"


### Tabla de contenidos

[TOC]



  [^ajax]: [Ajax](https://developer.mozilla.org/es/docs/Web/Guide/AJAX/Primeros_Pasos) AJAX (JavaScript Asíncrono y XML) es un término nuevo para describir dos capacidades de los navegadores que han estado presentes por años, pero que habían sido ignoradas por muchos desarrolladores Web, hasta hace poco que surgieron aplicaciones como Gmail, Google suggest y Google Maps. Las dos capacidades en cuestión son:
*La posibilidad de hacer peticiones al servidor sin tener que volver a cargar la página.* y *La posibilidad de analizar y trabajar con documentos XML.*


 [^javascript]: [Javascript](https://developer.mozilla.org/es/docs/Learn/Getting_started_with_the_web/JavaScript_basics) es un robusto lenguaje de programación que puede ser aplicado a un documento HTML y usado para crear interactividad dinámica en los sitios web. Fue inventado por Brendan Eich, co-fundador del proyecto Mozilla, Mozilla Foundation y la Corporación Mozilla .

[^jquery]: [jQuery](http://jquery.com/) jQuery es una biblioteca de JavaScript rápida, pequeña y rica en funciones. Hace cosas como el recorrido y manipulación de documentos HTML, manejo de eventos, animación, y Ajax mucho más simple con una API fácil de usar que funciona en una multitud de navegadores. Con una combinación de versatilidad y extensibilidad, jQuery ha cambiado la forma en que millones de personas escriben JavaScript.

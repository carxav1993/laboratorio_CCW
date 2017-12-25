# LABORATORIO - COMPUTACIÓN EN EL CLIENTE WEB

## Estudiante: Carlos Vega Oyola

![](https://i1.rgstatic.net/ii/profile.image/AS%3A526183737839616%401502463387127_xl/Carlos_Vega_Oyola.png)

El presente informe es una actividad denominada **Laboratorio:  Creación de una aplicación web en el cliente** de la asignatura **Computación en el Cliente Web** del ***Máster Universitario de Ingeniería del Software y Sistemas Informáticos***, en donde se detalla el uso de Jquery a lo largo de los años y como ha ido evolucionando para una mejor codificación y ahorro de tiempo al momento de efectuar la programación del mismo. 

Como ejemplo de ilustración se realizarán peticiones AJAX[^ajax] como normalmente se implementan con javascript nativo y con jquery de forma escalonada ante las mejoras que ha sufrido durante los años, para obtener chistes acerca de [Carlos Ray Norris](https://chucknorris.com/) (Chuck Norris) y además como se realizan actualmente. El sitio web que contiene los chistes acerca de Chuck Norris se denomina [The Internet Chuck Norris DataBase](http://www.icndb.com) y en su apartado [Api](http://www.icndb.com/api/) se muestra como acceder a dicha información.

Para la realización de este laboratorio se utilizarán:

- **Editor**: Visual Studio Code, para realizar la instalación y conocer como funciona -recomiendo el siguiente [enlace](https://code.visualstudio.com/docs) en donde se encontrará toda la información necesaria.
- **Framework Front-end**: Materialize CSS utilizado para representar los datos que se va a consumir mediante el api de los chistes, el sitio oficial de este framework se encontrará en el siguiente [enlace](http://materializecss.com/). 

> **Importante**
>  
> - Para la instalación del Framework Front-end **Materialize CSS**, se utilizará el CDN como se indica en su sitio web oficial, para más información dejo este [enlace](http://materializecss.com/getting-started.html).
> - Cabe mencionar que el Framework posee diferentes componentes CSS y documentación para implementarlos en una página web, dentro de esta actividad se utilizará un [slider](http://materializecss.com/media.html) donde se presentarán imágenes de Chuck Norris y como descripción el chiste que se obtiene a través del AJAX. 

### Comienzo del laboratorio

#### <i class="icon-file"></i> Ajax mediante Javascript nativo

1. Para el inicio de este laboratorio, se creará un archivo html denominado *1_javascript_ajax.html*.
2. Luego se añade en la cabecera de la página el enlace del archivo css y js respectivamente del Framework mediante CDN.
3. Se usa ***XMLHttpRequest*** para realizar la petición AJAX y obtener el resultado esperado, el código utilizado se observa a continuación.


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
El resultado de este apartado se muestra en el siguiente [enlace](http://investigacion.utmachala.edu.ec/laboratorio_CCW/1_javascript_ajax.html).
> Para complementar el código javascript nativo implementado para efectuar el primer apartado, sirvió de apoyo la página de la [W3School - Js][1].

___

#### <i class="icon-pencil"></i> Ajax mediante Jquery (2006)

1. Para este apartado, se creará un archivo html denominado *2_jquery_ajax.html*.
2. Luego se añade en la cabecera de la página el enlace del archivo css y js respectivamente del Framework mediante CDN.
3. Se usa `$.ajax(...)` para realizar la petición AJAX y obtener el resultado esperado, el código utilizado se observa a continuación.
4. El resultado es el mismo, solo que en código se puede observar notablemente la reducción de este mediante el uso de jquery, tal como se observa a continuación.

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

El resultado de este apartado se muestra en el siguiente [enlace](http://investigacion.utmachala.edu.ec/laboratorio_CCW/2_jquery_ajax.html).

> Para complementar el código jquery implementado para efectuar este apartado, sirvió de apoyo el sitio oficial de Jquery, específicamente la manipulación del [DOM][2].

___

#### <i class="icon-pencil"></i> Ajax mediante el plugin jquery a partir del 2014

1. Para este apartado, se creará un archivo html denominado *3_jquery_plugin_ajax.html*.
2. Luego se añade en la cabecera de la página el enlace del archivo css y js respectivamente del Framework mediante CDN.
3. Ahora se utilizará el plugin de Jquery que han incluido los respectivos datos la página de chistes, el mismo se encuentra en el siguiente [enlace](http://www.icndb.com/libraries/javascript-jquery-plugin/). Cabe recordar que para utilizar este plugin se debe ubicar en la cabecera del documento html encerrado entre las etiquetas en el atributo src `<script src="aqui"></script>`, el enlace de donde se obtendrá la información.
4. Para la obtención de la información, también la página ofrece métodos, el que se va a tomar es `$.icndb.getRandomJokes()`, que trae un número indicado de chistes.
5. El resultado es el mismo, solo que en código se puede observar notablemente la reducción de este mediante el uso del plugin jquery, tal como se observa a continuación.

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
El resultado de este apartado se muestra en el siguiente [enlace](http://investigacion.utmachala.edu.ec/laboratorio_CCW/3_jquery_plugin_ajax.html).

> Para complementar el código jquery implementado para efectuar este apartado, sirvió de apoyo el sitio oficial de Jquery, específicamente la manipulación del [DOM][2].

_____

#### <i class="icon-cog"></i> Web Components (presente)

1. Para este apartado, se creará un archivo html denominado *4_web_components.html*.
2. Luego se añade en la cabecera de la página el enlace del archivo css y js respectivamente del Framework Front-end mediante CDN.
3. Posteriormente se añade en la cabecera del documento HTML una etiqueta `<link>` y en el atributo ***rel*** se escribe ***"import"*** además del ***href*** que debe ir el enlace donde se tomará referencia el web component, quedando de la siguiente manera: `<link rel="import" href="https://raw.githubusercontent.com/erikringsmuth/chuck-norris-joke/master/chuck-norris-joke.html">`.
4. Para la obtención de la información únicamente se debe indicar las etiquetas `<chuck-norris-joke></chuck-norris-joke>`.
5. El resultado es el mismo, aunque en código queda muy simplificado a una única linea de etiqueta del html.

El resultado de este apartado se muestra en el siguiente [enlace](http://investigacion.utmachala.edu.ec/laboratorio_CCW/4_web_components.html).

> Mayor información de los web components, sírvase revisar el siguiente [enlace][3].

----
> Se recomienda revisar el sitio web [StackEdit.io][4] para aplicar sintaxis avanzadas sobre creación de documentos "markdown".

### Estadísticas

He considerado agregarle un plus a este apartado del performance al momento de cargar la página en los navegadores populare, segundos que tardan y número de peticiones que realizan.

#### Documento 1: 

Navegador| Segundos | Peticiones
-------- | :-------:| :--------:
Mozilla Firefox | 3.01 | 17
Google Chrome | 2.14 | 21

#### Documento 2: 
Navegador| Segundos | Peticiones
-------- | :-------:|:--------:
Mozilla Firefox | 3.13 | 17
Google Chrome | 2.81 | 21

#### Documento 3:
 
Navegador| Segundos | Peticiones
-------- | :-------:|:--------:
Mozilla Firefox | 5.07 | 17
Google Chrome | 3.95 | 21

#### Documento 4:
 
Navegador| Segundos | Peticiones
-------- | :-------:|:--------:
Mozilla Firefox | 6.55 | 17
Google Chrome | 6.30 | 21

> **Conclusión** Ante estos resultados (fue la primera que se tomó al momento de recargar la página usando la herramienta para desarrolladores que ofrecen los navegadores Google Chrome y Mozilla Firefox) se puede llegar a concluir que si bien es cierto Jquery facilita mucho en realizar múltiples acciones al momento de manipular el DOM que javascript nativo, pero nos cuesta un poco de rendimiento al momento de completar las peticiones, aunque sea mínimo y poco perceptible, lo es.
> Efectúe este análisis porqué en el foro que tenemos de la asignatura se había comentado acerca del rendimiento que penaliza el uso de Jquery. 
> Sin embargo, Jquery hoy es día es uno de los Framework más usado a nivel mundial, solucionando un sinnúmero de inconvenientes y logrando efectuar muchas acciones con pocas líneas de código, por ello está correcto su lema "Write less, do more"


### Tabla de contenidos

[TOC]



  [^ajax]: [Ajax](https://developer.mozilla.org/es/docs/Web/Guide/AJAX/Primeros_Pasos) AJAX (JavaScript Asíncrono y XML) es un término nuevo para describir dos capacidades de los navegadores que han estado presentes por años, pero que habían sido ignoradas por muchos desarrolladores Web, hasta hace poco que surgieron aplicaciones como Gmail, Google suggest y Google Maps. Las dos capacidades en cuestión son:
*La posibilidad de hacer peticiones al servidor sin tener que volver a cargar la página.* y *La posibilidad de analizar y trabajar con documentos XML.*


  [1]: https://www.w3schools.com/js/
  [2]: http://api.jquery.com/category/manipulation/ "Manipulación DOM"
  [3]: https://www.webcomponents.org/ "Web Components"
  [4]: https://stackedit.io
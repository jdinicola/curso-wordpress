# Referencia rápida de WordPress

## Jerarquía

Tipo de página | Intentos
--- | ---
404 | 404.php &rarr; index.php
Búsqueda | search.php &rarr; index.php
Taxonomía | taxonomy-**{tax}**-**{term}**.php &rarr; taxonomy-**{tax}**.php &rarr; taxonomy.php &rarr; archive.php &rarr; index.php
Home | home.php &rarr; index.php
Adjunto | **{mime-type}**.php &rarr; attachment.php &rarr; single.php &rarr; index.php
Entrada individual | single-**{tipo}**.php &rarr; single.php &rarr; index.php
Página estática | **{plantilla}**.php &rarr; page-**{slug}**.php &rarr; page-**{id}**.php &rarr; page.php &rarr; index.php
Categoría | category-**{slug}**.php &rarr; category-**{id}**.php &rarr; category.php &rarr; index.php
Etiqueta | tag-**{slug}**.php &rarr; tag-**{id}**.php &rarr; tag.php &rarr; archive.php &rarr; index.php
Autor | author-**{alias}**.php &rarr; author-**{id}**.php &rarr; author.php &rarr; archive.php &rarr; index.php
Fecha | date.php &rarr; archive.php &rarr; index.php
Archivo | archive.php &rarr; index.php

## Anatomía

### Estructura de directorio

<pre>
mi-tema
|  + css
|  |  - estilos.css
|  |  - ...
|  + fonts
|  |  - ...
|  + img
|  |  - ...
|  + js
|  |  - ...
|  + templates
|  |  - plantilla.php
|  |  - ...
|  - 404.php
|  - archive.php
|  - footer.php
|  - functions.php
|  - header.php
|  - index.php
|  - page.php
|  - screenshot.png
|  - single.php
|  - style.css
</pre>

### Declaración del tema (encabezado de la hoja de estilos)

<pre>
/*
	Theme Name: Mi Tema
	Theme URI: http://mipagina.com
	Author: Nombre Autor
	Author URI: http://mipagina.com
	Description: Descripción del tema
	Version: 1.0
*/
</pre>

### Declaración de plantillas de páginas

<pre>
/*
	Template name: Nombre de la plantilla
*/
</pre>

## Sintaxis de WordPress

### Invocar funciones de plantilla (_template tags_)

<pre>
&lt;?php nombre_funcion( argumentos ); ?&gt;
</pre>

### Invocar funciones condicionales (_conditional tags_)

<pre>
&lt;?php if ( nombre_funcion( argumentos ) ) : ?&gt;
		
	Instrucciones si verdadero
	
&lt;?php else : ?&gt;
		
	Instrucciones si falso

&lt;?php endif; ?&gt;
</pre>

### El bucle (_the loop_)

<pre>

&lt;?php if ( have_posts() ) : ?&gt;

	&lt;?php while ( have_posts() ) : the_post(); ?&gt;
	
		Instrucciones por cada entrada
	
	&lt;?php endwhile; ?&gt;

&lt;?php else : ?&gt;

	Instrucciones si no hay entradas

&lt;?php endif; ?&gt;
</pre>

### Añadir una acción e invocar una función

<pre>
// En el fichero functions.php

add_action( 'accion', 'nombre_funcion' );

function nombre_funcion( argumentos ) {

	// Instrucciones 

}
</pre>

### Añadir un filtro e invocar una función

<pre>
// En el fichero functions.php

add_filter( 'filtro', 'nombre_funcion' );

function nombre_funcion( entrada ) {

	// Instrucciones
	
	return $salida;

}
</pre>

## Funciones, acciones y filtros más comunes

### Funciones de plantilla (_template tags_)

Función | Descripción
--- | ---
`get_header()` | Incluye el fichero de la cabecera (header.php)
`get_sidebar()` | Incluye el fichero de la barra lateral (sidebar.php)
`get_footer()` | Incluye el fichero del pie (footer.php)
`get_comments_template()` | Incluye el fichero de comentarios (comments.php) si existe
`bloginfo()` | Devuelve información del sitio (detallado más adelante)
`wp_title()` | Muestra el título del sitio
`wp_nav_menu()` | Muestra los menús personalizados registrados
`dynamic_sidebar()` | Muestra las áreas de widgets registradas
`the_title()` | Muestra el título de la entrada o página
`the_content()` | Muestra el contenido de la entrada o página
`the_excerpt()` | Muestra el resumen de la entrada o página
`the_time()` | Muestra la fecha de la entrada o página
`the_permalink()` | Muestra el enlace permanente a la entrada o página
`the_category()` | Muestra las categorías a las que pertenece la entrada o página
`the_tags()` | Muestra las etiquetas de la entrada o página
`the_author()` | Muestra el autor de la entrada o página (por defecto, archive.php)
`the_author_posts_link()` | Muestra un link a una página con todas las entradas del autor
`the_search_query()` | Muestra los términos de la búsqueda 
`the_post_thumbnail()` | Muestra la imagen destacada de la entrada o página
`comments_link()` | Muestra un link a los comentarios de la entrada o página
`comments_number()` | Muestra el número de comentarios para una entrada o página
`next_posts_link()` | Muestra un link a la próxima entrada
`previous_posts_link()` | Muestra un link a la entrada anterior

[Referencia completa](http://codex.wordpress.org/Template_Tags)

### Función de información del sitio (bloginfo)

Función | Descripción
--- | ---
`bloginfo( 'language' )` | Devuelve el código de idioma
`bloginfo( 'charset' )` | Devuelve el juego de caracteres usado
`bloginfo( 'stylesheet_url' )` | Devuelve la URL de la hoja de estilos del tema actual
`bloginfo( 'name' )` | Devuelve el nombre del sitio especificado en los ajustes
`bloginfo( 'description' )` | Devuelve la descripción del sitio especificada en los ajustes
`bloginfo( 'url' )` | Devuelve la URL del sitio especificada en los ajustes 
`bloginfo( 'template_url' )` | Devuelve la URL del directorio del tema actual

[Referencia completa](http://codex.wordpress.org/Function_Reference/bloginfo)

### Funciones condicionales (_conditional tags_)

Función | Descripción
--- | ---
`is_home()` | Verifica si la página actual es la página de entradas (index.php)
`is_front_page()` | Verifica si la página actual es la frontal (especificada en los ajustes)
`is_single()` | Verifica si la página actual es individual
`is_page()` | Verifica si la página actual es una página
`is_category()` | Verifica si la página actual es una colección de alguna categoría
`is_tag()` | Verifica si la página actual es una colección de alguna etiqueta
`is_author` | Verifica si la página actual es una colección de entradas de algún autor
`is_month()` | Verifica si la página actual es una colección de entradas escritas en algún mes
`has_post_thumbnail()` | Verifica si la entrada o página tiene imagen destacada

[Referencia completa](http://codex.wordpress.org/Conditional_Tags)

### Acciones

Acción | Descripción
--- | ---
`init`| Ejecuta una función cuando WordPress se inicializa
`wp_enqueue_scripts`| Pone en cola los scripts que se cargarán en la página
`wp_head()` | Imprime, en la cabecera, código esencial para el funcionamiento de WP (justo antes `</head>`)
`wp_foot()` | Imprime, en el pie, código esencial para el funcionamiento de WP (justo antes `</body>`)
`register_nav_menus()`| Registra menús personalizados
`register_sidebar`()| Registra áreas de widgets
`add_theme_support()`| Añade soportes específicos al tema
`add_image_size()`| Añade tamaños de imágenes personalizados


[Referencia completa](http://codex.wordpress.org/Plugin_API/Action_Reference)

### Filtros

Filtro | Descripción
--- | ---
`the_title()` | Filtra el título de la entrada o página
`the_content()` | Filtra el contenido de la entrada o página
`the_excerpt()` | Filtra el resumen de la entrada o página
`pre_get_posts`| Filtra las entradas antes de enviarlas al bucle

[Referencia completa](http://codex.wordpress.org/Plugin_API/Filter_Reference)



































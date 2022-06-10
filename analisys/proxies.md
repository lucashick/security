# Proxies

Realizar el análisis de estos métodos desde el navegador puede ser engorroso, por lo que podemos recurrir a herramientas como Proxies. 

* [ZAP](https://www.zaproxy.org/)
* [Burp Suite](https://portswigger.net/burp)

Usamos la versión Community de Burp Suite que es gratuita, que la podremos obtener [aquí](https://portswigger.net/burp/releases/community/latest)

Para trabajar con Burp Suite, ZAP, o algún otro proxy se recomienda usar Firefox, ya que se puede configurar dentro del navegador. Chrome lleva directamente a la configuración de proxy de tu SO.  
__En las últimas versiones de burp suite, trae una opción de Launch Browser en la pestaña de Proxie, la misma nos lanzará una sesión de Chromium con todas las configuraciones que se mencionan a continuación, listo para empezar a trabajar.__

### Configuración
Una vez instalado y abierto Burp Suite, nos queda configurar el navegador. En Firefox vamos a opciones, buscamos la opción de Configuración de Proxy, configuramos el Proxy HTTP con 127.0.0.1, el puerto que luego vayamos a especificar dentro del proxy, que por defecto es 8080 y por último marcamos la casilla de usar también este proxy para FTP y HTTPS.

Ahora nos queda instalar el certificado de Burp Suite en Firefox. Para eso primero desactivamos el Intercept de Burp, nos dirigimos a la Pestaña superior Proxy, y luego a la pestaña inferior Intercept. Allí haremos click en el botón "Intecept is on", que cambiará a "is off". Luego ingresamos en nuestro navegador (Firefox) a http://burp/ y hacemos click en la parte "CA Certificate", lo cual descargará un archivo. Si no se muestra nada al ingresar es porque el proxy está mal configurado.

Por último instalamos el certificado en Opciones →  Certificados →  Ver Certificados →  Importar (Seleccionamos el archivo que acabamos de descargar)

__Podemos llegar a tener problemas si tenemos que trabajar en el localhost, para solucionar esto:__
* Loguear localhost en Burp desde firefox
* Ir a about:config
* network.proxy.allow_hijacking_localhost → true

### BurpSuite
Una vez realizados estos pasos, hay un paso que es opcional pero facilita mucho el trabajo: Nos dirigimos a la pestaña superior __Target__ y a la pestaña inferior __Scope__. Hacemos click en __Add__ y luego especificamos en la ventana que se abrió los datos sobre la página que nos interesa. Si no se sabe sobre alguno de los campos es mejor dejarlo en blanco.

Al hacer click en Ok se nos abrirá un mensaje que nos preguntará si se quiere que Burp deje de enviar los elementos fuera del Scope (es decir, todas las páginas que nosotros no especificamos en esta pestaña). Lo recomendable es apretar "Yes", para así evitar luego tener que ver peticiones de dominios que no nos interesan.

__Importante:__ Al estar utilizando una versión gratuita, los proyectos son temporales y se borra el progreso cuando cerramos Burp. Esto incluye lo que hayamos definido en el scope, el historial de peticiones, y la configuración del Listener

Luego, en la pestaña superior Proxy nos encontramos con 3 pestañas inferiores de interés:

#### Intercept
Encendiendo la opción para interceptar peticiones, cada petición que el navegador hubiese mandado, pasará por Burp antes de enviarse. Ahí mismo podemos decidir si queremos editarla (simplemente se escribe en el texto que se muestra), droppearla (es decir, no enviarla) con el botón Drop. Una vez editada (o también si se quiere enviar sin editar), se usa el botón Forward para enviarla. Si se desactiva la opción para interceptarlas, lo mismo podremos visualizar lo que se manda en la pestaña inferior HTTP History. 

#### HTTP History
Aquí es donde veremos cada una de las peticiones que se enviaron. Acá es donde sirve haber definido el Scope, ya que solo aparecerán las peticiones de los dominios que nosotros especificamos (si no se especifica nada, se muestran todas). Se puede hacer click derecho en cualquier petición, donde tendrán varias opciones para aplicarle. 

#### Options
Acá es donde se pueden configurar un montón de cosas, pero en un principio vamos a usar la parte de "Proxy Listeners" únicamente para configurar el proxy. Importante: Si el navegador no les carga ninguna página y les tira el error "El servidor proxy está rechazando las conexiones", recuerden que puede que tengan la configuración de Proxy prendida en el navegador o SO y su Proxy cerrado (o escuchando en un puerto distinto).


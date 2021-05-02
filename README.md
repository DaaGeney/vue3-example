# VUE 3 SINCE VUE 2

Actuamente tenemos a nuest alcance la version 3 de vue (Beta), una version que trae cambios interesantes que vienen con el objetivo de dar mas manejabilidad a los amantes de este framework progresivo. En este articulo te daremos una entrada a las principales novedades que trae esta nueva version y, acompañada de algunos ejemplos de como han cambiado las cosas en este framework. Para abarcar esto explicaremos los cambios mas importantes, empezando desde la reactividad en vue 3 hasta la nueva composition API, que se puede entender como el plato fuerte.

Para el desarrollo hay que mencionar que actualmente existen multiples formas de usar Vue en nuestros projectos, entre las que destacan en uso de cdn, npm o la instalacion del cli. Para los ejemplos aquí presentados se hará uso del CLI de vue, con la estructura:

![GitHub Logo](/article-vue3/assets/estructure.png)

Donde template contiene todas las etiquetas html y los elementos del Dom, scripts contiene la logica y styles la hoja de estilos de la aplicacion.

## Reactivity in vue 3
En vue 3 se implementa un cambio brutal en la forma de manejar estados locales, este nos presenta un cambio en su filosofia pasando de 'todo es reactivo' a 'indica lo reactivo', ¿De qué hablamos? miren a continuacion. 
Actualmente vue 2 posee la funcion data que es donde se almacenan todas las variables locales que manejará nuestra aplicacion, esta funcion tiene la caracteristica que todo aquellos que este dentro es reactivo (basta con definirlo dentro de esta funcion para que lo sea), es decir, que un cambio en estas automaticamente modificara el bundle de nuestra aplicacion. 

![GitHub Logo](/article-vue3/assets/data-method.png)

En la imagen anterior tenemos que el estado 'message' es reactivo, lo cual implica que un simple cambio en este se verá reflejado en el dom, el inconveniente viene cuando tenemos muchos elementos dentro de data() todos siendo reactivos al mismo tiempo, esto hace que el desarrollador pierda un poco de control sobre lo que realmente quiere que sea dinamico y lo que no, vue 3 presenta uno de los cambios mas notables al reemplazar completamente el metodo data por setup(), y con sigo la forma en la que usan los estados locales. En la composition API (de quien hablaremos a fondo mas adelante) se presentan algunas funciones como lo son 'ref' y 'reactive', que son aquellas que nos permiten definidir cuando queremos que una variable sea reactiva en nuestra aplicacion. *ref* nos permite definir variables reactivas de un solo valor, es decir, todas aquellas variables de tipo primitivo mientras que la funcion *reactive* nos permite crear todo un objeto reactivo, es decir, nos proporciona un objeto en el que la modificacion de cada una de sus propiedades se verán reflejadas en todas las secciones de nuestro codigo donde lo llamemos. Ademas de esto, la funcion setup nos permite devolver aquellas variables que realmente deseamos usar directamente en el template al incluirlas en el return. 

![GitHub Logo](/article-vue3/assets/setup-method.png)

En el ejemplo vemos como tenemos un estado local llamado message que al estar incluido dentro del return puede ser utilizado desde el template de nuestra aplicacio, y al cual al definirlo con la funcion ref nos garantiza que cualquier modificacion que sufra por medio su propiedad value (message.value) se verá reflejado en todo aquel lugar en nuestro codigo donde este sea usado. 

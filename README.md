# VUE 3 SINCE VUE 2

Actuamente tenemos a nuestro alcance la version 3 de vue (Beta), una version que trae cambios interesantes que vienen con el objetivo de dar mas manejabilidad a los amantes de este framework progresivo. En este articulo te daremos una entrada a las principales novedades que trae esta nueva version acompañada de algunos ejemplos de como han cambiado las cosas en este framework. Para abarcar esto explicaremos los cambios mas importantes, empezando desde la reactividad en vue 3 hasta la nueva composition API, que se puede entender como el plato fuerte.

Para el desarrollo hay que mencionar que actualmente existen multiples formas de usar Vue en nuestros projectos, entre las que destacan en uso de cdn, npm o la instalacion del cli, para los ejemplos aquí presentados se hará uso del CLI de vue, con la estructura de single file:

![Estructure vue](/article-vue3/assets/estructure.png)

Donde template contiene todas las etiquetas html y los elementos del Dom, scripts contiene la logica y styles la hoja de estilos de la aplicacion.

## Reactivity in vue 3
En vue 3 se implementa un cambio brutal en la forma de manejar estados locales, este nos presenta un cambio en su filosofia pasando de 'todo es reactivo' a 'indica lo reactivo', ¿De qué hablamos? miren a continuacion. 
Actualmente vue 2 posee la funcion data que es donde se almacenan todas las variables locales que manejará nuestra aplicacion, esta funcion tiene la caracteristica que todo aquellos que este dentro es reactivo (basta con definirlo dentro de esta para que lo sean), es decir, que un cambio modificara el bundle de nuestra aplicacion. 

![data](/article-vue3/assets/data-method.png)

En la imagen anterior tenemos que el estado 'message' es reactivo, lo cual implica que un simple cambio en este se verá reflejado en el dom, el inconveniente viene cuando tenemos muchos elementos dentro de data() todos siendo reactivos al mismo tiempo, esto hace que el desarrollador pierda un poco de control sobre lo que realmente quiere que sea dinamico y lo que no, vue 3 presenta uno de los cambios mas notables al reemplazar completamente el metodo data por setup(), y con sigo la forma en la que usan los estados locales. En la composition API se presentan algunas funciones como lo son 'ref' y 'reactive', que son aquellas que nos permiten definir cuando queremos que una variable sea reactiva en nuestra aplicacion. *ref* nos permite definir variables reactivas de un solo valor, es decir, todas aquellas variables de tipo primitivo, mientras que la funcion *reactive* nos permite crear todo un objeto reactivo, es decir, nos proporciona un objeto en el que la modificacion de cada una de sus propiedades se verán reflejadas en todas las secciones de nuestro codigo donde lo llamemos. Ademas de esto, la funcion setup nos permite devolver aquellas variables que realmente deseamos usar directamente en el template al incluirlas en el return. 

![setup](/article-vue3/assets/setup-method.png)

En el ejemplo vemos como tenemos un estado local llamado message que al estar incluido dentro del return puede ser utilizado desde el template de nuestra aplicacion, y al definirlo con la funcion ref nos garantiza que cualquier modificacion que sufra por medio su propiedad value (message.value) se verá reflejado en todo aquel lugar en nuestro codigo donde este sea usado. 

### Watch and computed

Aparte de esto, debemos recordar que vue 2 nos ofrece observadores para seguir el comportamiento de propiedades especificas, tales como watch and computed. Watch nos permite hacer total seguimiento a una propiedad y realizar una accion cada que esta varíe mientras que computed nos permite crear una propiedad conformada por dos variables y actualizarse cada vez que una de estas se vea modificada. 
En el siguiente ejemplo tenemos un nombre completo compuesto por a firsName and lastName, vemos la forma de manipulas esto directamente con un computed o por watch.

![watch-computed](/article-vue3/assets/watch-computed.png)

El problema está en que en la estructura actual de Vue elcodigo puede quedar muy poco legible y dificil de entender,tal como se muestra a continuación.

![vue ref](https://v3.vuejs.org/images/options-api.png)


Vue 3 nos invita a usar estas dos propiedades directamente dentro del setup, mejorando mucho la legibilidad pues no implica la creacion de secciones unitarias para cada variable por fuera del metodo principal. 
veamos la forma de escribir el ejemplo anterior con la logica de vue 3.

![watch-computed](/article-vue3/assets/watch-computes-vue3.png)

como vemos, el elemento fullname manejado por un computed pasa de ser manipulado como una funcion independiente a ser directamente nombrada como un atributo dentro del setup y directamente se le asigna el resultado de una funcion. 

### Methods 
De la misma forma en que vue 3 ha manipulado los wath and computed lo ha hecho con los metodos, actualmente vue 2 obliga a que estos esten definidos dentro de la seccion methods dando como resultado que todos estos podian ser llamados desde el template de forma magica. Siguiendo con la nueva filosofia de vue, estos tambien pasan a hacer parte del metodo setup y todos aquellos que requieran ser usados desde el template deberan ser definidos en el return.
Esta nueva forma de uso da via libre a que las funciones flechas entren en funcionamiento, ya que debido a la forma que se trataban en vue 2 su uso era casi impensado. 

## Composition API

Como hemo visto a lo largo de este articulo, desde el metodo setup hasta los ref hacen parte de esta nueva composition API, que hace una fuerte apuesta por darte total control al desarrollador a cerca de sobre que se comportamiento tendra cada cosa y sobre que se puede usar en el template y que no. La nueva composition api da un giro total en la forma de ver el codigo, mejorando desde la parte visual hasta la parte funcional en algunos casos (el ejemplo mas claro es el reemplazo de data por setup) pero aun así, Vue le da tiempo al cambio a los desarrolladores al no dejar deprecated lo que se conoce actualmente y dando la posibilidad de usar tanto la options APi como esta nueva composition.

### Ciclo de vida de los componentes
Actualmente los ciclos de vida, como todo en vue 2, estan aislados a su propia section: 

![lifecycle](/article-vue3/assets/lifecycle-vue2.png)

En vue 3 estos sufren un cambio minimo, pues su nombramiento sufre la agregacion de on antes de su nombre actual y pasan a ser invocados dentro del setup, de resto se puede asegurar que su funcionamiento sigue siendo el mismo a excepcion de beforeCreate and created ya que estos desaparecen y en la pagina de vue se nos indica lo siguiente: 
_*Because setup is run around the beforeCreate and created lifecycle hooks, you do not need to explicitly define them. In other words, any code that would be written inside those hooks should be written directly in the setup function.*_


![lifecycle](/article-vue3/assets/new-lifecycle.png)

### Tre Shaking

Definitivamente el equipo de Vue se dio cuenta que estaban llenando el arbol con muchas cosas opcionales que los desarrolladores no usarian, tal como todos los eventos del ciclo de vida, todas las variables reactivas y muchas de las funcionalidades que poseen; es por esto que esta vez optan por hacer que los desarrolladores se vean en la obligacion de importar todo aquello que deseen usar, lo cual claramente hace que tengamos un bundle mucho mas limpio en comparacion a vue 2.


## Conclusion
Vue 3 trae importantes mejoras en su forma de crear componentes, la composition API apunta a darle total manejo al desarrollador acerca de lo que está haciendo en todo momento, ademas de eso, al ser reescrito totalmente con typescript le da total soporte a este y abre la puerta a los amantes a este lenguaje de programacion. 
ademas la inclusion del metodo setup es una apuesta atrevida ya que invita a usar todo en el mismo sitio, lo cual puede que no a todos los desarrolladores les agrade. Podemos asegurar que vue apuesta a lo grande al no quedarse atras ante los hooks de react (muchas funciones de la composition API se sienten basadas en estos) y el renderizador Ivy de angular y nos queda esperar por su lanzamiento oficial a ver como su integracion del nuevo vuex 4 y todo el ecosistema conocido para vue logra hacer que mas personas se una a este team.


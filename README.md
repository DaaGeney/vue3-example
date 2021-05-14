# Vue 3, introduction.

Currently we have at our disposal the version 3 of vue (Beta), a version that offers us interesting changes that come with the objetive of giving more manageability to developers of this progressive framework. In this article we will give you an entry to the main novelties that this new version brings together with some examples of how some things have changed in this framework. . To cover this we will explain the most important changes, starting from the reactivity in vue 3 to the new composition API, which can be understood as the highlight.
For the development it should be mentioned that currently there are multiple ways to use Vue in our projects, among which the use of cdn, npm or the installation of the cli, for the examples presented here, the vue CLI will be used, with the structure from single file:

![Estructure vue](/article-vue3/assets/estructure.png)

Where template contains all the html tags and elements of the Dom, scripts contains the logic and styles the stylesheet of the application.

## Reactivity in vue 3
In vue 3 a brutal change is implemented in the way of handling local states, this presents us with a change in the philosophy going from 'everything is reactive' to 'indicates the reactive', what are we talking about? look below. Currently vue 2 has the data function, it is where all the local variables that our application will handle are stored, this function has the characteristic that all those that are inside are reactive (it is enough to define them within it to make them so), that a change will modify the bundle of our application. 

![data](/article-vue3/assets/data-method.png)

In the previous image we have that the 'message' state is reactive, which implies that a simple change in it will be reflected in the dom, the problem comes when we have many elements within data () all being reactive at the same time, this makes the developer lose a bit of control over what he really wants to be dynamic and what he doesn't, vue 3 introduces one of the most notable changes by completely replacing the data method with setup (), and with the way in which they use local states. In the composition API some functions such as 'ref' and 'reactive' are presented, which are those that allow us to define when we want a variable to be reactive in our application. ref allows us to define reactive variables of a single value, that is, all those variables of primitive type, while the reactive function allows us to create a whole reactive object, it provides us with an object in which the modification of each one of its properties will be reflected in all sections of our code where we call it. In addition to this, the setup function allows us to return those variables that we really want to use directly in the template by including them in the return.

Note: Vue 2 forces us to specify the context when using the local state and methods the component's own , adding 'This' when using them, Vue 3 loses that context and the use of 'This' becomes unnecessary at when using the elements of our component.

![setup](/article-vue3/assets/setup-method.png)

In the example we see how it has a local state called message and due to it is included in the return, can be used from the template of our application, and when defining it with the ref function, it guarantees that any modification suffered through its value (message.value) will be reflected in all place in our code where it is used.

### Watch and computed

we must remember that vue 2 offers us observers to follow the behavior of specific properties, such as watch and computed. Watch allows us to fully monitor a property and perform an action each time it changes, while computed allows us to create a property made up of two variables and update each time one of these is modified. In the following example we have a full name composed of a firsName and lastName, we see how you manipulate this directly with a computed or by watch. .

![watch-computed](/article-vue3/assets/watch-computed.png)

The problem is that in the current structure of Vue the code can be very difficult to understand, as shown below. 
Vue 3 invites us to use these two properties directly within the setup, greatly improving readability since it does not imply the creation of unit sections for each variable outside the main method. Let's see how to write the previous example with the logic of vue 3.

![watch-computed](/article-vue3/assets/watch-computes-vue3.png)

As we can see, the fullname element handled by a computed goes from being manipulated as an independent function to being directly named as an attribute within the setup and the result of a function is directly assigned to it.

### Methods 
In the same way that vue 3 has manipulated the wath and computed it has done it with the methods, currently vue 2 forces these to be defined within the methods section resulting in that all these could be called from the template magically. Continuing with the new philosophy of vue, these also become part of the setup method and all those that need to be used from the template must be defined in the return. This new way of use it gives way to the arrow functions to come into operation, due to the way they were treated in vue 2 their use was almost unthinkable.

## Composition API

As we have seen throughout this article, from the setup method to the refs they are part of this new composition API, which makes a strong commitment to give the developer full control over what behavior each thing will have and what it will be used in the template and what not. The new composition api takes a total turn in the way of seeing the code, improving from the visual part to the functional part in some cases (the clearest example is the replacement of data by setup) but even so, Vue gives time to change to the developers by not leaving deprecated what is currently known and giving the possibility of using both the options API and this new composition.

### Ciclo de vida de los componentes
Currently lifecycles, like everything in vue 2, are isolated to their own section:

![lifecycle](/article-vue3/assets/lifecycle-vue2.png)

In vue 3 these undergo a minimal change, since their naming suffers the addition of on before their current name and they become invoked within the setup, otherwise it can be ensured that their operation remains the same except for beforeCreate and created already that these disappear and in the vue page the following is indicated:
_*Because setup is run around the beforeCreate and created lifecycle hooks, you do not need to explicitly define them. In other words, any code that would be written inside those hooks should be written directly in the setup function.*_


![lifecycle](/article-vue3/assets/new-lifecycle.png)


### Tree Shaking

Definitely the Vuee team understood that they were filling the tree with many optional things that the developers would not use, such as all the life cycle events, all the reactive variables and many of the functionalities that they have; This is why they choose to make developers feel obliged to import everything they want to use, which clearly makes us have a much cleaner bundle compared to vue 2.


## Conclusion
Vue 3 brings important improvements in its way of creating components, the composition API aims to give full control to the developer about what he is doing at all times, in addition to that, being totally rewritten with typescript gives full support to this and opens the door to lovers of this programming language. In addition, the inclusion of the setup method is a daring bet since it invites you to use everything in the same place, which may not be pleasing to all developers. We can ensure that vue bets big by not falling behind the react hooks (many composition API functions feel based on these) and angular's ivy renderer. We can wait for its official launch to see how with the integration of the new vuex 4 and the entire known ecosystem of vue they manage to make more developers prefer to be in this team.



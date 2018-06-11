<div style="display: flex; align-items: center; justify-content: center; flex-direction: column">

![](images/vue.png)

# Vue.js Supercharged Crash Course

###### Hackathonners, Braga - 25 November 2017

</div>

---

<div style="display: flex; align-items: center; justify-content: center;">

<img src="images/profile2.jpg" style="width: auto; height: 300px; border-radius: 50%; margin-right: 50px">

<div class="display: flex; align-items: center; justify-content: center; flex-direction: column">

# Hugo Matalonga

Full Stack Developer

[http://hmatalonga.com](http://hmatalonga.com)

</div>

</div>

---
<!-- page_number: true -->

# What is Vue.js?

> Vue.js is an open-source progressive JavaScript framework for building user interfaces.

Core library focus on the view layer. 

Vue's design was partly inspired by the [MVVM pattern](https://en.wikipedia.org/wiki/Model_View_ViewModel).

Easily integrates with other libraries or existing projects.

Also great to create **Single-Page Applications**.

---

# First things first, a few basic concepts

---

# Hello World

## Declarative Rendering

```html
<div id="app">
  {{ message }}
</div>
```

```javascript
const app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

[https://jsfiddle.net/chrisvfritz/50wL7mdz/](https://jsfiddle.net/chrisvfritz/50wL7mdz/)

---

# Conditionals

```html
<div id="app-2">
  <span v-if="seen">Now you see me</span>
</div>
```

```javascript
const app2 = new Vue({
  el: '#app-2',
  data: {
    seen: true
  }
})
```

---
<!-- page_number: true -->

# Loops

```html
<div id="app-3">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```

```javascript
const app3 = new Vue({
  el: '#app-3',
  data: {
    todos: [
      { text: 'Learn JavaScript' },
      { text: 'Learn Vue' },
      { text: 'Build something awesome' }
    ]
  }
})
```

---
<!-- page_number: true -->

# Handling User Input

The `v-on` directive attachs event listeners that invoke methods on our Vue instances.

```html
<div id="app-4">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Reverse Message</button>
</div>
```

```javascript
const app4 = new Vue({
  el: '#app-4',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage() {
      this.message = 
        this.message.split('').reverse().join('')
    }
  }
})
```
---

# Two-Way Data Binding

```html
<div id="app-5">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```

```javascript
const app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue!'
  }
})
```
---

# Components 101

```javascript
// Define a new component called todo-item
Vue.component('todo-item', {
  template: '<li>This is a todo</li>'
})
```

```html
<ol>
  <!-- Create an instance of the todo-item component -->
  <todo-item></todo-item>
</ol>
```

---

```html
<div id="app-6">
  <ol>
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id">
    </todo-item>
  </ol>
</div>
```

```javascript
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
const app6 = new Vue({
  el: '#app-6',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Apples' }
    ]
  }
})
```
---

# Basics done. Now the Good Parts...

---

# Vue Instance

Every Vue application starts by creating a new Vue instance with the Vue function:

```javascript
const vm = new Vue({
  // options
})
```
[Vue Instance Properties](https://vuejs.org/v2/api/#Instance-Properties)

---

# Data and Methods

```javascript
// Our data object
let data = { a: 1 }
// The object is added to a Vue instance
let vm = new Vue({
  data: data
})
// These reference the same object!
vm.a === data.a // => true
// Setting the property on the instance
// also affects the original data
vm.a = 2
data.a // => 2
// ... and vice-versa
data.a = 3
vm.a // => 3
```

`data` - Vue's reactivity system (only) object

---

# Instance Lifecycle Hooks

```javascript
const vm = new Vue({
  
  // beforeCreate()
  // created()
  // beforeMount()
  // mounted()
  
  // beforeUpdate()
  // updated()
  
  // activated()
  // deactivated()
  
  // beforeDestroy()
  // destroyed()
  // errorCaptured()   (new in 2.5.0+)
  
})
```
**Don't use arrow functions on an options property or callback!**

[Lifecycle Diagram](https://vuejs.org/v2/guide/instance.html#Lifecycle-Diagram)

---

# Template Syntax

Under the hood, Vue compiles the templates into Virtual DOM render functions. Combined with the reactivity system, Vue is able to intelligently figure out the minimal number of components to re-render and apply the minimal amount of DOM manipulations when the app state changes.

---

# Interpolations

## Text

```html
<span>Message: {{ msg }}</span>

<span v-once>This will never change: {{ msg }}</span>
```
---

## Raw HTML

```html
<p>Using mustaches: {{ rawHtml }}</p>
<p>
  Using v-html directive:
  <span v-html="rawHtml"></span>
</p>
```
Dynamically rendering arbitrary HTML on your website can be very dangerous because it can easily lead to XSS vulnerabilities. Only use HTML interpolation on trusted content and never on user-provided content.

---

## Using JavaScript Expressions

### DO's

```html
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>
```

### DON'Ts

```html
<!-- this is a statement, not an expression: -->
{{ var a = 1 }}

<!-- flow control won't work, use ternary expressions -->
{{ if (ok) { return message } }}
```

You can also use some whitelist of globals such as `Math` and `Date`. However no user defined globals in template expressions.

---

# Directives

Directives are special attributes with the v- prefix.

Syntax:

`v-name:argument.modifier="value"`

`argument`, `modifier`, `value` can be optional.

Directive attribute values are expected to be a single JavaScript expression (with the exception for `v-for`).

```html
<p v-if="seen">Now you see me</p>
```
[Directives API](https://vuejs.org/v2/api/#Directives)

---

## Arguments

Some directives can take an "argument", denoted by a colon after the directive name. For example:

```html
<a v-bind:href="url"> ... </a>
```
---

## Modifiers

Modifiers are special postfixes denoted by a dot, which indicate that a directive should be bound in some special way. For example, the `.prevent` modifier tells the `v-on` directive to call `event.preventDefault()` on the triggered event:

```html
<form v-on:submit.prevent="onSubmit"> ... </form>
```
[`v-on` modifiers API](https://vuejs.org/v2/api/#v-on)

---

# Shorthands

Vue.js provides special shorthands for two of the most often used directives, `v-bind` and `v-on`:

## `v-bind`

```html
<!-- full syntax -->
<a v-bind:href="url"> ... </a>

<!-- shorthand -->
<a :href="url"> ... </a>
```

## `v-on`

```html
<!-- full syntax -->
<a v-on:click="doSomething"> ... </a>

<!-- shorthand -->
<a @click="doSomething"> ... </a>
```
---

# Computed Properties and Watchers

---

## Computed Properties

```html
<div id="example">
  {{ message.split('').reverse().join('') }}
</div>
```

At this point, the template is no longer simple and declarative.

That's why for any complex logic, you should use a **computed property**.

---

### Basic Example

```html
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversed }}"</p>
</div>
```

```javascript
const vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // a computed getter
    reversed() {
      // `this` points to the vm instance
      return this.message.split('').reverse().join('')
    }
  }
})
```
---

### Computed Caching vs Methods

Computed properties are cached based on their dependencies.

A computed property will only re-evaluate when some of its dependencies have changed. 

---

## Watchers

```html
<div id="watch-example">
  <p>
    Ask a yes/no question:
    <input v-model="question">
  </p>
  <p>{{ answer }}</p>
</div>
```

[Javascript code](https://vuejs.org/v2/guide/computed.html#Computed-vs-Watched-Property)

---

# Class and Style Bindings

---

## Binding HTML Classes

### Object Syntax

```html
<div v-bind:class="{ active: isActive }"></div>
```
`active` class will be determined by the truthiness of the data property `isActive`.

### Array Syntax

```html
<div v-bind:class="[activeClass, errorClass]"></div>
```
Toggle class:

```html
<div v-bind:class="[isActive ? activeClass : '',
			       errorClass]"></div>
```
---

# Conditional Rendering

---

## `v-if`, `v-else`, `v-else-if`

```html
<h1 v-if="ok">Yes</h1>

<h1 v-if="ok">Yes</h1>
<h1 v-else>No</h1>

<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```
You can also use these on `<template>` (conditional groups).

---

## `v-show`

Another option for conditionally displaying an element is the v-show directive.

```html
<h1 v-show="ok">Hello!</h1>
```

The difference is that an element with `v-show` will always be rendered and remain in the DOM; `v-show` only toggles the `display` CSS property of the element.

Note that `v-show` doesnâ€™t support the `<template>` element, nor does it work with `v-else`.

---

## `v-if` vs `v-show`

`v-if` is **lazy**: if the condition is false on initial render, it will not do anything - the conditional block wonâ€™t be rendered until the condition becomes true for the first time.

In comparison, `v-show` is much simpler - the element is always rendered regardless of initial condition, with CSS-based toggling.

## `v-if` with `v-for`

When used together with `v-if`, `v-for` has a higher priority than `v-if`. 

---

# List Rendering (Quick examples)

---

## Mapping an Array to Elements with `v-for`

```html
<ul id="example-1">
  <li v-for="item in items">
    {{ item.message }}
  </li>
</ul>
```

```javascript
const example1 = new Vue({
  el: '#example-1',
  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```
---

## Scope Parent Properties

```html
<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```

## `v-for` with an Object

```html
<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
```
---

## Displaying Filtered/Sorted Results

```html
<li v-for="n in even(numbers)">{{ n }}</li>
```

```javascript
data: {
  numbers: [ 1, 2, 3, 4, 5 ]
},
computed: {
  evenNumbers() {
    return this.numbers.filter(function (number) {
      return number % 2 === 0
    })
  }
}
```

## `key`

```html
<div v-for="item in items" :key="item.id">
  <!-- when your list render output rely on 
  child component state or temporary DOM state. -->
</div>
```
---

## `v-for` with a Range

```html
<div>
  <span v-for="n in 10">{{ n }} </span>
</div>
```

## `v-for` on a `<template>`

```html
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider"></li>
  </template>
</ul>
```

## `v-for` with `v-if`

When they exist on the same node, `v-for` has a higher priority than `v-if`! That means the `v-if` will be run on each iteration of the loop separately. 

---

# Transitions

---

## Enter/Leave & List Transitions

Vue provides a `transition` wrapper component, allowing you to add entering/leaving transitions for any element or component in the following contexts:

- Conditional rendering (using `v-if`)
- Conditional display (using `v-show`)
- Dynamic components
- Component root nodes

---

```html
<div id="demo">
  <button v-on:click="show = !show">
    Toggle
  </button>
  <transition name="fade">
    <p v-if="show">hello</p>
  </transition>
</div>
```

```javascript
new Vue({
  el: '#demo',
  data: {
    show: true
  }
})
```

```css
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to {
  opacity: 0
}
```

---

# Filters

Vue.js allows you to define filters that can be used to apply common text formatting.

```html
<!-- in mustaches -->
{{ message | capitalize }}

<!-- in v-bind -->
<div v-bind:id="rawId | formatId"></div>
```
---

You can define a local filter:

```javascript
filters: {
  capitalize(value) {
    if (!value) return ''
    value = value.toString()
    return value.charAt(0).toUpperCase() + 
    	   value.slice(1)
  }
}
```
or define a filter globally:

```javascript
Vue.filter('capitalize', function (value) {
  if (!value) return ''
  value = value.toString()
  return value.charAt(0).toUpperCase() + value.slice(1)
})
```

Filters can be chained and take arguments:

```javascript
{{ message | filterA | filterB }}

{{ message | filterA('arg1', arg2) }}
```

---

# Note: Vue with Laravel

```html
<template id="tasks-template">
  <h1>My Tasks</h1>
  <ul class="list-group">
    <li class="list-group-item" v-for="task in list">
      @{{ task.body }}
    </li>
  </ul>
</template>
```
Don't parse and ignore the blade template there.

---

# What's next?

- Single File Components
- Mixins, Custom directives, Plugins
- Routing
- State Management
- Server-Side Rendering
- Tooling (Unit testing, production deployment, typescript support, vue-cli, Vue DevTools, etc.)
- Supporting libraries (Nuxt.js, Weex, etc.)
- ...

---

# That's all. Thanks.
# Question time!

# Vue de A à Z

---

From a Vue instance, there are many properties.

## data()

"data" holds variables that can be used in the template.

```js
export default {
  data() {
    return {
        variableOne: 'valueOne'
        variableTwo: 'valueTwo'
    };
  },
};
```

## methods

"methods" holds functions that can be triggered from the template, when an event occurs for example.

We can call variables from "data" using the keyword "this".

Never use arrow functions in the methods property, once the "this" keyword won't work.

```js
export default {
	methods: {
		myMethod: function () {
			this.variableFromData;
		},
	},
};
```

## data-binding (directive)

In the template, in order to use variables inside an attribute ("href", for example), we can't put directly the variable or even the {{variable}}.

```js
    <a v-bind:href="variable"> Click me </a>
    // or
    <a :href="variable"> Click me </a>
```

## v-on (directive)

Takes the regular javascript events ('click', 'mouseover', 'change', 'keydown'...)

```js
<button v-on:click="handleClick"> Click me </button>
```

the event can be accessed as an argument to the function :

```js
export default {
	methods: {
		handleClick: function (event) {
			// this is gonna be the event of the click

			console.log(event);
		},
	},
};
```

## event modifiers

like the preventDefault() in Vanilla JS, modifiers of the event can be added

We have to put it after a dot on the v-on:

```js
<button v-on:click.once="method"> Click Me </button>
```

Many modifiers exist :

- once
- stop (stop propagation)
- prevent (prevent default in forms)

## key modifiers

Works the same way as event modifiers but linked to a specific key. When a an event is done with a specific key :

```js
<button v-on:click.ctrl="method"> Click me </button>
```

Several key modifiers are available :

- enter
- tab
- delete
- esc
- space
- up
- down
- left
- right
- ctrl
- alt
- shift
- meta

## v-model

Serves to link in realtime an input value to a variable. "two way data binding"

```html
<input type="text" v-model="value" />
```

```js
export default {
	data() {
		return {
			value: '',
		};
	},
};
```

The variable value will update in realtime dependin on the input

## v-once

States that the any dynamic data should only be evaluated once.

## Insert pure Html

```html
<div v-html="variableThatHoldsHtml">{{variableThatHoldsHtml}}</div>
```

## Methods, Computed and Watch

### Methods

Holds funtions that will be triggered when called (on events mainly, or calling it imediately in the template as data binding)

If data binding: method will be executed any time something changes.

Use methods mostly for events or for data that you want to be reloaded every time.

### Computed

Serves as data binding.

Computed properties are only re-evaluated if one of their "used values" changed.

**Use ir for data that depends on other data**

### Watch

Holds functions with the same name as data or computed properties. These functions will be fired any time the data changes.

It is not used in the template.

Use for any non-data update you want to make.

## Conditional class

```html
<div class="fixedClass" :class="{ myClass : boolean }"></div>
```

## Conditional display

v-if="boolean"

v-else-if="boolean"

v-else="boolean"

## v-for

```html
<ul>
	<li v-for="element in array">{{element}}</li>
</ul>
```

With indexes :

```html
<ul>
	<li v-for="(element, index) in array">{{index}} - {{element}}</li>
</ul>
```

With objects :

```html
<ul>
	<li v-for="(value, property) in object">{{property}} : {{value}}</li>
</ul>
```

Double loop :

```html
<ul>
	<li v-for="object in array">
		<div v-for="(value, prop) in object">{{prop}} : {{value}}</div>
	</li>
</ul>
```

---

### Send data from child to parent

In the child, we can call a method that "emits" an event.

```js

// IN THE CHILD

<template>
	<a class="btn" @click="sendToParent"> Click me </a>
</template>

<script>
	export default {
		methods: {
			sendToParent: function(){
				this.$emit('nameOfTheEvent', 'data')
			}
		}
	}
</script>

// IN THE PARENT

<p v-on:nameOfTheEvent="methodOfParent($event)"> </p>
// The $event represents the data sent by the child

methodOfParent(data){
	// Use the data
}

```

## Event BUS

---

### Slot

Slot serves as a "placeholder" in the child for content from the parent.

```js
// 
```
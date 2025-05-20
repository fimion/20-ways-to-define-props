---
# You can also start simply with 'default'
theme: ./theme
layout: intro
title: Welcome to Slidev
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)

# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: fade
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
lineNumbers: true
---

# 20 Ways to Define Props in Vue

<div></div>

# From Mundane to Unhinged

Alex Riviere  
Senior Frontend Developer at Hygiena  
bsky: [@dangitalex.wtf](https://bsky.app/profile/dangitalex.wtf)  
mastodon: [@fimion@notacult.social](https://notacult.social/@fimion)  
blog: [Alex.Party](https://alex.party)  

---
layout: quote
---

> "Did you see what this jackwagon did?"

-[Homer Gaines](https://bsky.app/profile/xirclebox.com)

---
layout: intro
---

# Generic Prop Definition

---
layout: cover
lineNumbers: true
---

## Generic Prop Definition

````md magic-move

```vue {all|3}
<script>
export default {
	props:['modelValue', 'name', 'options']
}
</script>
```

```vue {4}
<script>
export default {
	props:[
	'modelValue',
	'name',
	'options',
	]
}
</script>
```

````
---
layout: intro
---

# Add Some Types

---
layout: cover
---

## Add Some Types

````md magic-move

```vue {all|4|5|6|all}
<script>
export default {
	props: {
		modelValue: [String, Number],
		name: String,
		options: Object,
	}
}
</script>
```

```vue {all|4-7|6|8-11|10|12-15|14|all}
<script>
export default {
	props: {
		modelValue:{
			type: [String, Number],
			required: true,
		},
		name:{
			type: String,
			default: "Le Poisson Steve",
		},
		options: {
			type: Object,
			default: ()=>({}),
		},
	}
}
</script>
```

```vue {all|10|all}
<script>
export default {
	props: {
		modelValue:{
			type: [String, Number],
			required: true,
		},
		name:{
			type: String,
			default: ()=>"Le Poisson Steve",
		},
		options: {
			type: Object,
			default: ()=>({}),
		},
	}
}
</script>
```

```vue {all|13|15-18|all}
<script>
export default {
	props: {
		modelValue:{
			type: [String, Number],
			required: true,
		},
		name:{
			type: String,
			default: ()=>"Le Poisson Steve",
		},
		options: {
			type: [Object, null],
			default: ()=>({}),
			validator(value, props){
			    if(value.id && typeof value.id !== "number") return false;
			    return true;
			}
		},
	}
}
</script>
```

```vue {all|1|2|4-6|12|all}
<script lang="ts">
import { type PropType } from "vue";

type Options = {
    id?:number;
}

export default {
	props: {
		/* ... `modelValue` and `name` removed for example */
		options: {
			type: [Object, null] as PropType<Options|null>,
			default: ()=>({}),
			validator(value, props){
			    if(value.id && typeof value.id !== "number") return false;
			    return true;
			}
		},
	}
}
</script>
```
````

---
layout: intro
---

# Run Time vs. Build Time

---
layout: two-cols-header
---

## Run Time vs. Build Time

::left::

<v-clicks>

### Run Time

</v-clicks>

<v-clicks>

- Is interpreted in the browser
- can be used in any JS interpreter
- Does not require a build step

</v-clicks>

::right::

<v-clicks>

### Build Time

</v-clicks>

<v-clicks>

- Is the actual build step
- Can be a compiler macro to create run time code
- will not work outside of having a build step

</v-clicks>

---
layout: intro
---

# Single File Component Magic


<v-clicks>

<div class="text-5xl">

`<script setup>`

</div>

</v-clicks>

---
layout: cover
---

## Single File Component Magic `<script setup>`

````md magic-move

```vue {all|1|2|all}
<script setup>
	const props = defineProps(['modelValue', 'name', 'options'])
</script>
```

```js {all|3|4|5|all}
const __sfc__ = {
  __name: 'MyComponent',
  props: ['modelValue', 'name', 'options'],
  setup(__props) {
	const props = __props
    return () => {}
  }
}
__sfc__.__file = "src/MyComponent.vue"
export default __sfc__
```

```vue 
<script setup>
const props = defineProps({
    modelValue: [String, Number],
    name: String,
    options: Object,
});
</script>
```

```vue
<script setup>
const props = defineProps({
    modelValue:{
        type: [String, Number],
        required: true,
    },
    name:{
        type: String,
        default: "",
    },
    options: {
        type: Object,
        default: ()=>({}),
    },
});
</script>
```

```vue
<script setup>
const props = defineProps({
    modelValue:{
        type: [String, Number],
        required: true,
    },
    name:{
        type: String,
        default: ()=>"",
    },
    options: {
        type: Object,
        default: ()=>({}),
    },
});
</script>
```

```vue
<script setup>
const props = defineProps({
    modelValue:{
        type: [String, Number],
        required: true,
    },
    name:{
        type: String,
        default: ()=>"",
    },
    options: {
        type: [Object, null],
        default: ()=>({}),
        validator(value, props){
            if(value.id && typeof value.id !== "number") return false;
            return true;
        }
    },
});
</script>
```

```vue
<script setup lang="ts">
import { type PropType } from "vue";

type Options = {
    id?:number;
}

const props = defineProps({
    /* ... `modelValue` and `name` removed for example */
    options: {
        type: [Object, null] as PropType<Options|null>,
        default: ()=>({}),
        validator(value, props){
            if(value.id && typeof value.id !== "number") return false;
            return true;
        }
    },
});
</script>
```

````

---
layout: intro
---

# Get Funky With TypeScript

---
layout: cover
---

## Get Funky With TypeScript

````md magic-move

```vue 
<script setup lang="ts">
import {type PropType} from "vue"
type Options = {
    id?:number;
}
const props = defineProps({
    modelValue: [String, Number],
    name: String,
    options: Object as PropType<Options>,
});
</script>
```

```vue {all|5-9|6|7|8|all}
<script setup lang="ts">
type Options = {
    id?:number;
}
const props = defineProps<{
    modelValue: string|number;
    name: string,
    options: Options,
}>();
</script>
```

```js {all|6|7|8|all}
/** Dev Build **/
import { defineComponent as _defineComponent } from 'vue'
const __sfc__ = /*#__PURE__*/_defineComponent({
  __name: 'MyComponent',
  props: {
    modelValue: { type: [String, Number], required: true },
    name: { type: String, required: true },
    options: { type: Object, required: true }
  },
  setup(__props, { expose: __expose }) {
    __expose();
    const props = __props;
    const __returned__ = { props }
    Object.defineProperty(__returned__, '__isScriptSetup', { enumerable: false, value: true })
    return __returned__
  }
})
__sfc__.__file = "src/MyComponent.vue"
export default __sfc__
```

```js
/** Production Build **/
import { defineComponent as _defineComponent } from 'vue'
const __sfc__ = /*#__PURE__*/_defineComponent({
  __name: 'MyComponent',
  props: {
    modelValue: {},
    name: {},
    options: {}
  },
  setup(__props) {
    const props = __props;
    return () => {}
  }
})
__sfc__.__file = "src/MyComponent.vue"
export default __sfc__
```
```vue
<script setup lang="ts">
type Options = {
    id?:number;
}
const props = defineProps<{
    modelValue: string|number;
    name: string,
    options: Options,
}>();
</script>
```

```vue
<script setup lang="ts">
type Options = {
    id?:number;
}

type Props = {
    modelValue: string|number;
    name: string,
    options: Options,
}

const props = defineProps<Props>();
</script>
```

```vue {all|12|13|14-17|all|7|8,15|9,16|all}
<script setup lang="ts">
type Options = {
    id?:number;
}

type Props = {
    modelValue: string|number;
    name?: string,
    options?: Options,
}

const props = withDefaults(
    defineProps<Props>(),
    {
        name:"",
        options: ()=>({})
    }
);
</script>
```
````

---
layout: cover
---

## Get Funky With TypeScript

### `BaseProps.ts`
```ts {all|4-7|9-12|all}
export type Options = {
  id?:number;
}
export interface BaseProps {
  name?: string;
  options?: Options
}

export const BasePropsDefaults = {
  name: "",
  options: ()=>({}),
}
```

---
layout: cover
---

## Get Funky With TypeScript
```vue {all|2|4-6|9-11|all}
<script setup lang="ts">
import {type BaseProps, BasePropsDefaults} from "./BaseProps.ts";

interface Props extends BaseProps{
	modelValue: string|number;
}
const props = withDefaults(
	defineProps<Props>(),
	{
		...BasePropsDefaults,
	}
);
</script>
```
---
layout: intro
---

# modelValue is Complicated


---
layout: cover
---

## modelValue is Complicated

````md magic-move

```vue
<script setup lang="ts">
import {type BaseProps, BasePropsDefaults} from "./BaseProps.ts";

interface Props extends BaseProps{
	modelValue: string|number;
}
const props = withDefaults(
	defineProps<Props>(),
	{
		...BasePropsDefaults,
	}
);
</script>
```

```vue {all|4-6|all}
<script setup lang="ts">
import {type BaseProps, BasePropsDefaults} from "./BaseProps.ts";

const model = defineModel({
    type: [String,Number]
})

const props = withDefaults(
	defineProps<BaseProps>(),
	{
		...BasePropsDefaults,
	}
);
</script>
```

```vue {all|4-5|7-8|all}
<script setup lang="ts">
import {type BaseProps, BasePropsDefaults} from "./BaseProps.ts";

/** creates entries in `props` and `emits` */
const model = defineModel<string|number>()

/** lets you do things like this: */
model.value = 0;

const props = withDefaults(
	defineProps<BaseProps>(),
	{
		...BasePropsDefaults,
	}
);
</script>
```

````

---
layout: intro
---

# For the React Fans - JSX

---
layout: cover
---

## JSX

````md magic-move

```tsx
export const MyComponent = defineComponent((props)=>{
	return ()=><div>{props.propName}</div>
},{
	props: ['propName'],
})
```

```tsx
export const MyComponent = defineComponent((props)=>{
	return ()=><div>{props.propName}</div>
},{
	props: {
		propName: String
	},
});
```

```tsx
export const MyComponent = defineComponent((props)=>{
	return ()=><div>{props.propName}</div>
},{
	props: {
		propName:{
			type: String,
			default: "",
		}
	},
});
```

```tsx
export const MyComponent = defineComponent((props)=>{
	return ()=><div>{props.propName}</div>
},{
	props: {
		propName:{
			type: String,
			default: ()=>"",
		}
	},
});
```

```tsx
export const MyComponent = defineComponent((props)=>{
	return ()=><div>{props.propName}</div>
},{
	props: {
		propName:{
			type: String,
			default: ()=>"",
			validator: (value)=>typeof value === "string",
		}
	},
});
```
````

---
layout: cover
---

# Let's Talk About <span class="font-mono">$attrs</span>

<v-clicks>

- Always passed from parent as extra attributes
- Automatically set on root element of component
- Can be set on specific element with `v-bind="$attrs"`

</v-clicks>

---
layout: intro
---

<div class="text-center block">
<h1>The Unhinged Hypothetical</h1>
</div>

<div class="text-center block">
<span class="font-mono text-6xl leading-20" v-click>useMagicProps()</span>
</div>


---
layout: cover
---

## Magic Props

````md magic-move

```vue
<script>

export default {
    setup(){
        const propsDef = ref([]);
        return { propsDef }
    }
}

</script>
```

```vue
<script>
import { useMagicProps } from "use-magic-props";
export default {
    setup(){
        const propsDef = ref([]);
        useMagicProps(propsDef);
        return { propsDef }
    }
}
</script>
```


```vue
<script>
import { useMagicProps } from "use-magic-props";
export default {
    setup(){
        const propsDef = ref([]);
        useMagicProps(propsDef);
        propsDef.value.push("message");
        return { propsDef }
    }
}
</script>
```

```vue
<script>
import { useMagicProps } from "use-magic-props";
export default {
    setup(){
        const propsDef = ref([]);
        useMagicProps(propsDef);
        propsDef.value.push("message");
        return { propsDef }
    }
}
</script>
<template>
    <div>
    {{$props.message}}
    </div>
</template>
```

```vue
<script>
import { useMagicProps } from "use-magic-props";
export default {
    setup(){
        const propsDef = ref([]);
        useMagicProps(propsDef);
        propsDef.value.push("message");
        return { propsDef }
    }
}
</script>
<template>
    <div>
    {{message}}
    </div>
</template>
```

````

---
layout: intro
---



<div class="text-center block">
<v-switch>
    <template #0>
        <h1>The Unhinged Hypothetical</h1>    
    </template>
    <template #1>
        <h1>The Unhinged <del>Hypothetical</del></h1>
    </template>
</v-switch>
</div>

<div class="text-center block">
<span class="font-mono text-6xl leading-20">useMagicProps()</span>
</div>

---
layout: center
---

`npm install use-magic-props`

---
layout: default
---

<UseMagicPropsDemo />

---
layout: intro
---

## So why would you want to do this?

<div></div>

<v-click>

# You Don't.

</v-click>

---
layout: intro
---


# Thank You.


Alex Riviere  
Senior Frontend Developer at Hygiena  
bsky: [@dangitalex.wtf](https://bsky.app/profile/dangitalex.wtf)  
mastodon: [@fimion@notacult.social](https://notacult.social/@fimion)  
blog: [Alex.Party](https://alex.party)  

---
# You can also start simply with 'default'
theme: excali-slide
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
---

# 20 Ways to Define Props in Vue

---
layout: quote
---

<blockquote class="text-6xl w-half">

"Did you see what this jackwagon did?"

-[Homer Gaines](https://bsky.app/profile/xirclebox.com)

</blockquote>

---
layout: intro
---

# Generic Prop Definition

---
layout: cover
---

## Generic Prop Definition

```vue
<script>
export default {
	props:['modelValue', 'name', 'options']
}
</script>
```

---
layout: intro
---

# Add Some Types

---
layout: cover
---

## Add Some Types

````md magic-move

```vue
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

```vue
<script>
export default {
	props: {
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
	}
}
</script>
```

```vue
<script>
export default {
	props: {
		modelValue:{
			type: [String, Number, Object],
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
	}
}
</script>
```

```vue
<script>
export default {
	props: {
		propName:{
			type: String,
			default: ()=>"",
			validator: (value, props)=>typeof value === "string",
		}
	}
}
</script>
```
````

---
layout: intro
---

# Single File Component Magic

<div></div>

## `<script setup>`

---
layout: cover
---

## Single File Component Magic `<script setup>`

````md magic-move

```vue
<script setup>
	const props = defineProps(['propName'])
</script>
```

```vue
<script setup>
const props = defineProps({
		propName: String
	});
</script>
```

```vue
<script setup>
const props = defineProps({
		propName:{
			type: String,
			default: "",
		}
	});
</script>
```

```vue
<script setup>
const props = defineProps({
		propName:{
			type: String,
			default: ()=>"",
		}
	});
</script>
```

```vue
<script setup>
const props = defineProps({
		propName:{
			type: String,
			default: ()=>"",
			validator: (value)=>typeof value === "string",
		}
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
const props = defineProps<{propName: string}>();
</script>
```

```vue
<script setup lang="ts">
const props = withDefaults(
	defineProps<{propName?: string}>(),
	{
		propName: "",
	}
);
</script>
```

```vue
<script setup lang="ts">
const props = withDefaults(
	defineProps<{propName?: string}>(),
	{
		propName: ()=>"",
	}
);
</script>
```

```vue
<script setup lang="ts">
interface Props {
	propName?: string;
}
const props = withDefaults(
	defineProps<Props>(),
	{
		propName: ()=>"",
	}
);
</script>
```

```vue
<script setup lang="ts">
import {type BaseProps, BasePropsDefault} from "./BaseProps.ts";

interface Props extends BaseProps{
	propName?: string;
}
const props = withDefaults(
	defineProps<Props>(),
	{
		...BasePropsDefault,
		propName: ()=>"",
	}
);
</script>
```
````

---
layout: intro
---

## For the React Fans - JSX

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
layout: intro
---

<div class="text-center block">
<h1>Let's Get Unhinged</h1>
</div>
<div class="text-center block">
<span class="font-mono text-6xl leading-20" v-click>useMagicProps()</span>
</div>
<div class="text-center block">
<span class="text-4xl" v-click>Please don't use this.</span>
</div>

---

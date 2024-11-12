---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# some information about your slides (markdown enabled)
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

```vue
<script>
export default {
	props:['propName']
}
</script>
```

---

````md magic-move
```vue
<script>
export default {
	props: {
		propName: String
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
			default: "",
		}
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
		}
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
			validator: (value)=>typeof value === "string",
		}
	}
}
</script>
```
````

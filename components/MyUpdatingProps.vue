<script setup>
import {ref} from "vue"
import {useMagicProps} from "use-magic-props"

defineProps({
  test: {
    type: Boolean,
  },
})
const propsDef = ref(["message"])
useMagicProps(propsDef)
</script>
<template>
  <div class="wrapper">
    <div>
      <button class="button" type="button" @click="propsDef.push('class')">add "class" to <code>propsDef</code></button>
      <button class="button" type="button" @click="propsDef = propsDef.filter((el=>el!=='class'))">remove "class" from <code>propsDef</code></button>
    </div>
    <h2><code>$props.message</code></h2>
    <p>{{ $props.message }}</p>
    <h2><code>message</code></h2>
    <p>{{ message }}</p>
    <p></p>
    <h2><code>propsDef</code></h2>
    <pre>{{ propsDef }}</pre>
    <h2><code>$props</code></h2>
    <pre>{{ $props }}</pre>
  </div>
</template>

<style scoped>
:where(.wrapper) {
  border: 3px dodgerblue solid;
  padding: 1rem;
  column-count: 2;
}

button{
  padding-inline: 1ch;
  margin-inline: 1ch;
  border: 3px hotpink ridge;
}
</style>

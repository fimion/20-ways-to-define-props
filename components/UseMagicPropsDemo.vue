<script setup lang="ts">
import MyUpdatingProps from "./MyUpdatingProps.vue";
import {ref} from "vue";
const thing = ref("Hello World");
</script>

<template>
  <div class="container">
    <h1 class="title">{{thing}}</h1>
    <div/>
    <label>Update message: <input v-model="thing"></label>
    <MyUpdatingProps class="class-from-parent" :message="thing" />
  </div>
</template>

<style scoped>
input{
  border: 1px indigo solid;
}
.class-from-parent{
  border-color: orange;
}
</style>

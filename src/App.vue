<template>
  <section class="container">
    <h2>{{ name }}</h2>
    <h3>{{ age }}</h3>
    <button @click="changeAge">Change age</button>
  </section>
</template>

<script setup>
import { ref, reactive, isReactive, isRef, toRefs } from 'vue';

const user = reactive({
  name: 'Illiada',
  age: 23,
});
const exampleString = 'Hello Composition API';
const exampleRefString = ref('Hello Composition API');

console.log('Is user ref: ', isRef(user));
console.log('Is user reactive: ', isReactive(user));
console.log('Is exampleString ref: ', isRef(exampleString));
console.log('Is exampleRefString ref: ', isRef(exampleRefString));
const userRefs = toRefs(user);
const { name, age } = userRefs;
name.value = 'Illiada Boiko';

console.log(user);

setTimeout(() => {
  user.name = 'Illia';
  user.age++;
}, 3000);

function changeAge() {
  age.value++;
  user.age++; 
}
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>
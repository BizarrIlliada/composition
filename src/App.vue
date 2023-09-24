<template>
  <section class="container">
    <h2>{{ name }}</h2>
    <h3>{{ age }}</h3>
    <button @click="changeAge">Change age</button>
    <div>
      <input type="text" placeholder="First Name" v-model="firstName">
      <input type="text" placeholder="Last Name" ref="lastNameInput" @input="setLastName">
      <button @click="setLastName">Set last name</button>
    </div>
    <div>
      <p>
        {{ fullName }}
      </p>
      <p>
        {{ firstName }}
      </p>
    </div>
    <p>{{ 'Dogs gender is ' + gender }}</p>
    <img height="200" src="https://encrypted-tbn3.gstatic.com/licensed-image?q=tbn:ANd9GcQTIg6tKhqwokMCnry9-wROugbZ1GrgDbAz3dOwgGkHGAFFFuRmzCILAkDx9HKufB2kKO726I6fWLMcgsQ" alt="Dog">
    <UserData 
      :name="name"
      :lastName="lastName"
      class="test"
      fallThroughAttr="someText"
      @myEmittedFunction="console.log($event)"
    >
      <template #title>
        Title
      </template>
      <template #subtitle>
        <label for="test">Test</label>
        <input id="test" type="text" placeholder="Subtitle">
      </template>
      <div>{{ 123 }}</div>
    </UserData>
  </section>
</template>

<script setup>
import { ref, reactive, isReactive, isRef, toRefs, computed, isReadonly, watch, provide } from 'vue';

import UserData from './components/UserData.vue';

const user = reactive({
  name: 'Illiada',
  age: 23,
});
const gender = ref('Male');
const exampleString = 'Hello Composition API';
const exampleRefString = ref('Hello Composition API');

console.log('Is user ref: ', isRef(user));
console.log('Is user reactive: ', isReactive(user));
console.log('Is exampleString ref: ', isRef(exampleString));
console.log('Is exampleRefString ref: ', isRef(exampleRefString));
const userRefs = toRefs(user);
const { name, age } = userRefs;
name.value = 'Illiada Boiko';

const firstName = ref('');
const lastName = ref('');
const lastNameInput = ref(null);

const fullName = computed(() => firstName.value + ' ' + lastName.value);

console.log(user);
console.log('Is fullName readonly: ', isReadonly(fullName));

setTimeout(() => {
  user.name = 'Illia';
  user.age++;
}, 3000);

setTimeout(() => {
  gender.value = 'Female'
}, 5000);

function changeAge() {
  age.value++;
  user.age++; 
}

watch(fullName, (newVal, oldVal) => {
  console.log('New fullName: ', newVal);
  console.log('Old fullName: ', oldVal);
})

watch([age, gender], (newValues, oldValues) => {
  console.log('Age or gender was changed!');
  console.log(newValues);
  console.log(oldValues);
})

function setLastName() {
  lastName.value = lastNameInput.value.value;
}

provide('age', age);
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
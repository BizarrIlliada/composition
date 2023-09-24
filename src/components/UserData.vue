<template>
  <div>
    <svg class="gb_i" focusable="false" viewBox="0 0 24 24"><path d="M6,8c1.1,0 2,-0.9 2,-2s-0.9,-2 -2,-2 -2,0.9 -2,2 0.9,2 2,2zM12,20c1.1,0 2,-0.9 2,-2s-0.9,-2 -2,-2 -2,0.9 -2,2 0.9,2 2,2zM6,20c1.1,0 2,-0.9 2,-2s-0.9,-2 -2,-2 -2,0.9 -2,2 0.9,2 2,2zM6,14c1.1,0 2,-0.9 2,-2s-0.9,-2 -2,-2 -2,0.9 -2,2 0.9,2 2,2zM12,14c1.1,0 2,-0.9 2,-2s-0.9,-2 -2,-2 -2,0.9 -2,2 0.9,2 2,2zM16,6c0,1.1 0.9,2 2,2s2,-0.9 2,-2 -0.9,-2 -2,-2 -2,0.9 -2,2zM12,8c1.1,0 2,-0.9 2,-2s-0.9,-2 -2,-2 -2,0.9 -2,2 0.9,2 2,2zM18,14c1.1,0 2,-0.9 2,-2s-0.9,-2 -2,-2 -2,0.9 -2,2 0.9,2 2,2zM18,20c1.1,0 2,-0.9 2,-2s-0.9,-2 -2,-2 -2,0.9 -2,2 0.9,2 2,2z"></path></svg>
    <hr>
    <h2>
      <slot name="title"></slot>
    </h2>
    <h3>
      <slot name="subtitle"></slot>
    </h3>
    <p>UserData component:</p>
    <h2>{{ name }}</h2>
    <h3>{{ age }}</h3>
    <p>{{ fullName }}</p>
    <slot></slot>
    <button @click="myEmit">Emit</button>
  </div>
</template>

<script setup>
import {
  computed,
  defineProps,
  defineEmits,
  defineSlots,
  useAttrs,
  useSlots,
  inject,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
} from 'vue';

const props = defineProps({
  name: {
    type: String
  },
  // age: {
  //   type: Number
  // },
  lastName: {
    type: String
  },
});
const emits = defineEmits();

const attrs = useAttrs();

const slots = defineSlots();
const slots2 = useSlots();

const fullName = computed(() => props.name + ' ' + props.lastName);

console.log('Props: ', props);
console.table('Emits: ', emits);

console.log('Attrs: ', attrs);

console.log('Slots: ', slots);
console.log('Slots2: ', slots2);
console.log('slots === slots2: ', slots === slots2);
console.dir(useSlots);
console.dir(defineSlots);

console.log(slots.title());
console.log(slots.subtitle());
console.log(slots2.default());
console.log(slots2.title());

function myEmit() {
  emits('myEmittedFunction', 'Hello Vue! It\'s my emitted event!!!');
}

const age = inject('age');

onBeforeMount(() => {
  console.log('onBeforeMount');
});
onMounted(() => {
  console.log('onMounted');
});
onBeforeUpdate(() => {
  console.log('onBeforeUpdate');
});
onUpdated(() => {
  console.log('onUpdated');
});
onBeforeUnmount(() => {
  console.log('onBeforeUnmount');
});
onUnmounted(() => {
  console.log('onUnmounted');
});
</script>

<!--
  data() {...} ===> ref(), reactive()

  methods() { doSmth() { ... } } ===> function doSmth() { ... }

  computed(): { val() { return... } } ===> const val = computed(() => { return... })

  watch: { ... } ===> watch(dep, (val, oldVal) => { ... })

  provide: { ... } / inject: [] ===> provide(key, val) / const val = inject(key)
-->

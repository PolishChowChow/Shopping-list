<script setup lang="ts">
import { ref } from "vue";

const { onSubmit } = defineProps<{ onSubmit: (name: string) => void }>();
const nameRef = ref("");
const inputRef = ref<HTMLInputElement | null>(null);

const submitHandler = () => {
  onSubmit(nameRef.value);
  nameRef.value = "";
  inputRef.value?.focus();
};
</script>

<template>
  <form @submit.prevent="() => submitHandler()">
    <input type="text" v-model="nameRef" ref="inputRef" />
    <button type="submit">+</button>
  </form>
</template>

<style scoped></style>

<script setup lang="ts">
import { TaskType } from "../types/task";
import Task from "./Task.vue";
const { tasks } = defineProps<{ tasks: TaskType[] }>();
</script>

<template>
  <h2>Tasks</h2>
  <Task v-for="task in tasks" :key="task.id" :task="task" />
</template>

<style scoped></style>

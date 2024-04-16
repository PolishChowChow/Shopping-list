<script setup lang="ts">
import { TaskType } from '../types/task';

const { task } = defineProps<{task: TaskType}>()
</script>

<template>
    <div class="taskContainer">
        <div class="content">
            {{ task.name }}
        </div>
        <div>
            Delete
        </div>
    </div>

</template>

<style scoped>
    .taskContainer {
        display: flex;
        align-items: center;
        gap: 10px;
    }
    .taskContainer .content {
        flex: 1
    }
</style>

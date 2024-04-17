<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { TaskType } from '../types/task';

const { task } = defineProps<{task: TaskType}>()
const isEditable = ref(false)
const inputRef = ref("")
const editTask = () => {
    isEditable.value = false
}
const toggleForm = () => {
    isEditable.value = true
}
onMounted(()=>{
    inputRef.value = task.name
})
</script>

<template>
    <div class="taskContainer">
        <div class="content" v-if="!isEditable" @click="toggleForm">
            {{ task.name }}
        </div>
        <form @submit.prevent="editTask" v-if="isEditable">
            <input type="text" name="taskName" v-model="inputRef"/>
            <button type="submit">Save</button>
        </form>
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

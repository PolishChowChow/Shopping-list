<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { TaskType } from '../types/task';
import { useMutation, useQueryClient } from '@tanstack/vue-query';
import axios from 'axios';
const { task } = defineProps<{task: TaskType}>()
const client = useQueryClient()
const { mutateAsync: deleteTask } = useMutation({
    mutationFn: async(id: string) => {
        console.log(id)
        const response = await axios.delete(`http://localhost:3000/tasks/${id}`)
        return response.data.status
    },
    onSuccess: () => {
        client.invalidateQueries({
            queryKey: ["tasks"]
        })
    }
})

const isEditable = ref(false)
const inputRef = ref("")
const editTask = () => {
    isEditable.value = false
}
const toggleForm = () => {
    isEditable.value = true
}

onMounted(()=>{
    console.log(task.id);
    
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
        <div @click="() => deleteTask(task.id)">
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

<script setup lang="ts">
import { useMutation, useQuery, useQueryClient } from "@tanstack/vue-query";
import axios, { AxiosError } from "axios";
import TaskLists from "./components/TaskLists.vue";
import { TaskType } from "./types/task";
import Form from "./components/Form.vue";

const queryClient = useQueryClient()
const { data } = useQuery<TaskType[], AxiosError>({
  queryKey: ["tasks"],
  queryFn: async () => {
    const response = await axios.get("http://localhost:3000/tasks");
    console.log(response.data)
    return response.data
  },
});
const { mutateAsync } = useMutation({
  mutationFn: async(name: string) => {
    const response = await axios.post("http://localhost:3000/tasks",{
      name
    })
    return response.data.status
  },
  onSuccess: () => {
    queryClient.invalidateQueries({
      queryKey: ["tasks"]
    })
  }
})
const onSubmit = (name: string) => {
  if(name.trim().length !== 0){
    mutateAsync(name)
  }
}

</script>

<template>
  <div>
    <TaskLists :tasks="data as TaskType[]" />
    <Form :on-submit="onSubmit" />
  </div>
</template>

<style scoped></style>

<script setup>
import { reactive } from 'vue'
import { Inertia } from '@inertiajs/inertia'

defineProps({
  errors: Object
})

const form = reactive({
  title: null,
  content: null
})

const submitFunction = () => {
  Inertia.post('/inertia', form)
}
</script>

<template>
  <form @submit.prevent="submitFunction" class="m-2">
    <div v-if="errors.title">{{ errors.title }}</div>
    <input type="text" name="title" v-model="form.title" class="m-2"><br>
    <div v-if="errors.content">{{ errors.content }}</div>
    <input type="text" name="content" v-model="form.content" class="m-2"><br>
    <button class="bg-gray-200 p-2">送信</button>
  </form>
</template>
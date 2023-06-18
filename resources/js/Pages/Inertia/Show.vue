<script setup>
import { Inertia } from '@inertiajs/inertia'

defineProps({
  id: String,
  blog: Object
})

const deleteConfirm = (id) => {
  Inertia.delete(`/inertia/${id}`, {
    onBefore: () => confirm('本当に削除しますか?')
  })
}
</script>

<template>
  <div class="mx-2">
    <p>ID：{{ id }}</p>
    <p>タイトル：{{ blog.title }}</p>
    <button class="my-4 py-2 px-4 bg-red-500 text-white" @click="deleteConfirm(blog.id)">削除</button>
  </div>
</template>

<style scoped></style>
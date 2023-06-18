<script setup>
import { Link } from '@inertiajs/vue3'

defineProps({
  blogs: Array
})
</script>

<template>
  <div>
    <div v-if="$page.props.flash.message">【{{ $page.props.flash.message }}】<br></div>
    <ul class="m-4">
      <li v-for="blog in blogs" :key="blog.id" class="flex">
        <p class="w-32">件名: <Link class="text-blue-400" :href="route('inertia.show', {id: blog.id })">{{ blog.title }}</Link></p>
        <p>本文: {{ blog.content }}</p>
      </li>
    </ul><br>
    <Link as="button" method="get" :href="route('inertia.create')" class="my-4 mx-2 py-2 px-4 bg-gray-200">登録ページへ</Link>
  </div>
</template>

<style scoped></style>
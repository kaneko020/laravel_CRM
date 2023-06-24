<script setup>
</script>

<template>
  <div v-if="$page.props.flash.status === 'success'" class="bg-gray-400 text-white mb-4 p-2 rounded">
    {{ $page.props.flash.message }}
  </div>
  <div v-if="$page.props.flash.status === 'danger'" class="bg-gray-700 text-white mb-4 p-2 rounded">
    {{ $page.props.flash.message }}
  </div>
</template>
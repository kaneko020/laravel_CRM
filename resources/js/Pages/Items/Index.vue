<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue'
import { Head, Link } from '@inertiajs/vue3'
import FlashMessage from '@/Components/FlashMessage.vue'

defineProps({
  items: Array
})
</script>

<template>
  <Head title="商品一覧" />

  <AuthenticatedLayout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        商品一覧
      </h2>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
          <div class="py-8 px-16 text-gray-900">
            <section class="text-gray-600 body-font container mx-auto">
              <FlashMessage />
              <div class="flex mb-4 w-full mx-auto">
                <Link
                  as="button"
                  :href="route('items.create')"
                  class="flex ml-auto text-gray-800 bg-gray-100 py-2 px-6 rounded drop-shadow hover:bg-gray-400 hover:text-white"
                >
                  商品登録
                </Link>
              </div>
              <div class="w-full mx-auto overflow-auto">
                <table class="table-auto w-full text-left whitespace-no-wrap">
                  <thead>
                    <tr class="title-font tracking-wider font-medium text-sm text-gray-900 bg-gray-200">
                      <th class="w-[10%] px-4 py-3 font-medium">ID</th>
                      <th class="w-[50%] px-4 py-3 font-medium">商品名</th>
                      <th class="w-[20%] px-4 py-3 font-medium">価格</th>
                      <th class="w-[20%] px-4 py-3 font-medium">ステータス</th>
                    </tr>
                  </thead>
                  <tbody>
                    <Link
                      as="tr"
                      v-for="item in items"
                      :key="item.id"
                      :href="route('items.show', { item: item.id })"
                      class="bg-gray-50 odd:bg-white hover:bg-gray-100 cursor-pointer "
                    >
                      <td class="px-5 py-3 border-b border-gray-300">{{ item.id }}</td>
                      <td class="px-5 py-3 border-b border-gray-300">{{ item.name }}</td>
                      <td class="px-5 py-3 border-b border-gray-300">{{ item.price }}円</td>
                      <td class="px-5 py-3 border-b border-gray-300">
                        <span v-if="item.is_selling == 1">販売中</span>
                        <span v-if="item.is_selling == 0">停止中</span>
                      </td>
                    </Link>
                  </tbody>
                </table>
              </div>
            </section>
          </div>
        </div>
      </div>
    </div>
  </AuthenticatedLayout>
</template>

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue'
import { Head, Link } from '@inertiajs/vue3'
import { Inertia } from '@inertiajs/inertia'

defineProps({
  item: Object
})

const deleteItem = (id) => {
  Inertia.delete(route('items.destroy', { item: id }), {
    onBefore: () => confirm('本当に削除しますか?')
  })
}
</script>

<template>
  <Head title="商品詳細" />

  <AuthenticatedLayout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        商品詳細
      </h2>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
          <section class="text-gray-600 body-font relative">
            <div class="container px-5 py-8 mx-auto">
              <div class="lg:w-1/2 md:w-2/3 mx-auto">
                <div class="flex flex-wrap -m-2">
                  <div class="p-2 w-full">
                    <div class="relative">
                      <label class="leading-7 text-sm text-gray-600">商品名</label>
                      <div item="name" class="w-full bg-opacity-50 rounded border border-gray-300 text-base text-gray-700 py-1 px-3 leading-8">
                        {{ item.name }}
                      </div>
                    </div>
                  </div>
                  <div class="p-2 w-full">
                    <div class="relative">
                      <label class="leading-7 text-sm text-gray-600">商品メモ</label>
                      <div id="memo" class="w-full bg-opacity-50 rounded border border-gray-300 h-32 text-base text-gray-700 py-1 px-3 leading-6 whitespace-pre-line">
                        {{ item.memo }}
                      </div>
                    </div>
                  </div>
                  <div class="p-2 w-full">
                    <div class="relative">
                      <label class="leading-7 text-sm text-gray-600">商品価格</label>
                      <div id="price" class="w-full bg-opacity-50 rounded border border-gray-300 text-base text-gray-700 py-1 px-3 leading-8">
                        {{ item.price }}
                      </div>
                    </div>
                  </div>
                  <div class="p-2 w-full">
                    <div class="relative">
                      <label class="leading-7 text-sm text-gray-600">ステータス</label>
                      <div id="status" class="w-full bg-opacity-50 rounded border border-gray-300 text-base text-gray-700 py-1 px-3 leading-8">
                        <span v-if="item.is_selling == 1">販売中</span>
                        <span v-if="item.is_selling == 0">停止中</span>
                      </div>
                    </div>
                  </div>
                  <div class="p-2 w-full flex justify-between">
                    <button
                      @click="deleteItem(item.id)"
                      class="bg-gray-300 text-gray-900 py-2 px-8 rounded text-lg drop-shadow hover:bg-gray-500 hover:text-white"
                    >
                      削除
                    </button>
                    <Link
                      as="button"
                      :href="route('items.edit', { item: item.id })"
                      class="bg-gray-100 text-gray-800 py-2 px-8 rounded text-lg drop-shadow hover:bg-gray-500 hover:text-white"
                    >
                      編集
                    </Link>
                  </div>
                </div>
              </div>
            </div>
          </section>
        </div>
      </div>
    </div>
  </AuthenticatedLayout>
</template>

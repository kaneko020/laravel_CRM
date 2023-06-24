<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue'
import { Head, Link } from '@inertiajs/vue3'
import FlashMessage from '@/Components/FlashMessage.vue'
import Pagination from '@/Components/Pagination.vue'
import { ref } from 'vue'
import { Inertia } from '@inertiajs/inertia';


const props = defineProps({
  customers: Object
})

const search = ref('')

const searchCustomers = () => {
  Inertia.get(route('customers.index', { search: search.value }))
}

</script>

<template>
  <Head title="顧客一覧" />

  <AuthenticatedLayout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        顧客一覧
      </h2>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
          <div class="py-8 px-16 text-gray-900">
            <section class="text-gray-600 body-font container mx-auto">
              <FlashMessage />
              <div class="flex justify-between mb-4 w-full mx-auto">
                <div class="flex">
                  <input
                    type="text"
                    name="search"
                    v-model="search"
                    class="rounded-l border-r-0 border-gray-300 focus:outline-none focus:ring-0 focus:border-gray-300"
                  >
                  <button
                    class="bg-gray-200 text-gray-700 py-2 px-4 rounded-r border border-gray-300 hover:bg-gray-400 hover:text-white"
                    @click="searchCustomers"
                  >
                    検索
                  </button>
                </div>
                <Link
                  as="button"
                  :href="route('customers.create')"
                  class="flex ml-auto text-gray-800 bg-gray-100 py-2 px-6 rounded drop-shadow hover:bg-gray-400 hover:text-white"
                >
                  顧客登録
                </Link>
              </div>
              <div class="w-full mx-auto overflow-auto">
                <table class="table-auto w-full text-left whitespace-no-wrap">
                  <thead>
                    <tr class="title-font tracking-wider font-medium text-sm text-white bg-gray-500">
                      <th class="w-[16%] px-4 py-3 font-medium">ID</th>
                      <th class="w-[28%] px-4 py-3 font-medium">氏名</th>
                      <th class="w-[28%] px-4 py-3 font-medium">カナ</th>
                      <th class="w-[28%] px-4 py-3 font-medium">電話番号</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="customer in customers.data" :key="customer.id" class="odd:bg-gray-100">
                      <td class="px-5 py-3 border-b border-gray-300">{{ customer.id }}</td>
                      <td class="px-5 py-3 border-b border-gray-300">{{ customer.name }}</td>
                      <td class="px-5 py-3 border-b border-gray-300">{{ customer.kana }}</td>
                      <td class="px-5 py-3 border-b border-gray-300">{{ customer.tel }}</td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </section>
            <Pagination class="flex justify-center mt-12" :links="customers.links"></Pagination>
          </div>
        </div>
      </div>
    </div>
  </AuthenticatedLayout>
</template>

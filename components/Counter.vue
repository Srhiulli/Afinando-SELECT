<script setup lang="ts">
import { ref, onMounted } from 'vue'

// Simulando dados das tabelas
const contactTable = ref([
  { id: '478982xu2hi3wp382492', name: 'Alice' },
  { id: '94827sxi3829wi123092', name: 'Bob' }
])

const tagsTable = ref([
  { contact_id: '478982xu2hi3wp382492', tag: 'Premium' },
  { contact_id: '94827sxi3829wi123092', tag: 'Free' }
])

const showJoinArrow = ref(false)

// Exibindo a seta após carregar a página
onMounted(() => {
  setTimeout(() => {
    showJoinArrow.value = true
  }, 1000)
})
</script>

<template>
  <div class="flex justify-center items-center min-h-screen bg-gray-100">
    <!-- Tabela Contact -->
    <div class="w-1/3 p-4">
      <h2 class="text-lg font-bold mb-2 text-center">Tabela Contact</h2>
      <table class="table-auto w-full bg-white rounded-lg shadow-lg border border-gray-200">
        <thead>
          <tr class="bg-blue-200">
            <th class="px-4 py-2">Contact ID</th>
            <th class="px-4 py-2">Name</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="contact in contactTable" :key="contact.id" class="contact-row">
            <td class="px-4 py-2">{{ contact.id }}</td>
            <td class="px-4 py-2">{{ contact.name }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Seta de Join -->
    <div class="w-1/6 flex justify-center items-center relative">
      <div v-if="showJoinArrow" class="join-arrow"></div>
    </div>

    <!-- Tabela Tags -->
    <div class="w-1/3 p-4">
      <h2 class="text-lg font-bold mb-2 text-center">Tabela Tags</h2>
      <table class="table-auto w-full bg-white rounded-lg shadow-lg border border-gray-200">
        <thead>
          <tr class="bg-green-200">
            <th class="px-4 py-2">Contact ID</th>
            <th class="px-4 py-2">Tag Name</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="tag in tagsTable" :key="tag.contact_id" class="tags-row">
            <td class="px-4 py-2">{{ tag.contact_id }}</td>
            <td class="px-4 py-2">{{ tag.tag }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.join-arrow {
  width: 0;
  height: 0;
  border-top: 20px solid transparent;
  border-bottom: 20px solid transparent;
  border-left: 20px solid blue;
  animation: fadeIn 1s ease-in-out forwards;
}

.contact-row {
  animation: fadeIn 1s ease-in-out forwards;
}

.tags-row {
  animation: fadeIn 1s ease-in-out 1.5s forwards;
}
</style>
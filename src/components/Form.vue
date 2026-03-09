<template>
  <form @submit.prevent="handleSubmit"
        class="w-full max-w-md bg-white p-6 rounded-lg shadow-md space-y-4">

    <h2 class="text-2xl font-semibold text-gray-800 text-center">Обратная связь</h2>

    <div>
      <label class="block text-sm font-medium text-gray-700">Имя</label>
      <input
        v-model="form.firstName"
        type="text"
        placeholder="Введите имя"
        class="mt-1 block w-full border border-gray-300 rounded-md p-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
      />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700">Фамилия</label>
      <input
        v-model="form.lastName"
        type="text"
        placeholder="Введите фамилию"
        class="mt-1 block w-full border border-gray-300 rounded-md p-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
      />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700">Номер телефона</label>
      <input
        v-model="form.phone"
        type="tel"
        placeholder="+998 XX XXX XXXX"
        class="mt-1 block w-full border border-gray-300 rounded-md p-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
      />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700">Email</label>
      <input
        v-model="form.email"
        type="email"
        placeholder="example@mail.com"
        class="mt-1 block w-full border border-gray-300 rounded-md p-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
      />
    </div>

    <button
      type="submit"
      class="w-full bg-blue-600 text-white font-semibold py-2 rounded-md hover:bg-blue-700 transition"
    >
      Отправить
    </button>

  </form>
</template>

<script setup>
import { reactive } from 'vue'

const form = reactive({
  firstName: '',
  lastName: '',
  phone: '',
  email: '',
})

const handleSubmit = () => {
  if (!form.firstName || !form.lastName || !form.phone || !form.email) {
    alert('Пожалуйста, заполните все поля!')
    return
  }

  console.log('Форма отправлена:', form)

  alert('Спасибо! Форма отправлена.')

  form.firstName = ''
  form.lastName = ''
  form.phone = ''
  form.email = ''
}
</script>

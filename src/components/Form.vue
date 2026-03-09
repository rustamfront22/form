<template>
  <section class="form-page">
    <!-- Background -->
    <div class="background-layer">
      <div class="blob blob-1"></div>
      <div class="blob blob-2"></div>
      <div class="blob blob-3"></div>
      <div class="grid-layer"></div>
      <div class="overlay-layer"></div>
    </div>

    <!-- Notification -->
    <transition name="fade-scale">
      <div
        v-if="notification.show"
        class="fixed top-6 left-1/2 z-[100] w-[calc(100%-32px)] max-w-md -translate-x-1/2"
      >
        <div
          :class="[
            'rounded-2xl border px-5 py-4 shadow-2xl backdrop-blur-xl',
            notification.type === 'error'
              ? 'border-red-400/30 bg-red-500/10 text-red-100'
              : 'border-emerald-400/30 bg-emerald-500/10 text-emerald-100'
          ]"
        >
          <div class="flex items-start gap-3">
            <div
              :class="[
                'mt-0.5 flex h-10 w-10 shrink-0 items-center justify-center rounded-full',
                notification.type === 'error'
                  ? 'bg-red-500/20 text-red-300'
                  : 'bg-emerald-500/20 text-emerald-300'
              ]"
            >
              <svg
                v-if="notification.type === 'error'"
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
                stroke-width="2"
              >
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v3.75m0 3.75h.007M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>

              <svg
                v-else
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
                stroke-width="2"
              >
                <path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75l2.25 2.25L15 9.75m6 2.25a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>

            <div class="flex-1">
              <h3 class="text-sm font-bold">
                {{ notification.type === 'error' ? 'Проверьте форму' : 'Успешно' }}
              </h3>
              <p class="mt-1 text-sm leading-6 opacity-90">
                {{ notification.message }}
              </p>
            </div>

            <button
              @click="notification.show = false"
              class="rounded-full p-1 text-white/70 transition hover:bg-white/10 hover:text-white"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
        </div>
      </div>
    </transition>

    <!-- Form -->
    <div class="relative z-10 w-full px-4 py-10 sm:px-6">
      <div
        class="mx-auto w-full max-w-xl rounded-[30px] border border-white/10 bg-white/10 p-5 shadow-[0_20px_80px_rgba(0,0,0,0.45)] backdrop-blur-2xl sm:p-8 animate-fade-up"
      >
        <div class="pointer-events-none absolute inset-0 rounded-[30px]"></div>

        <div class="mb-5 flex justify-center">
          <div class="rounded-full border border-cyan-300/20 bg-cyan-400/10 px-4 py-1 text-[11px] font-semibold uppercase tracking-[0.28em] text-cyan-200">
            Premium Form
          </div>
        </div>

        <div class="text-center">
          <h2 class="text-3xl font-black tracking-tight text-white sm:text-5xl">
            Обратная связь
          </h2>
          <p class="mx-auto mt-3 max-w-md text-sm leading-6 text-slate-300 sm:text-base">
            Оставьте свои данные, и мы свяжемся с вами максимально быстро
          </p>
        </div>

        <form @submit.prevent="handleSubmit" class="mt-8 space-y-5">
          <!-- Имя -->
          <div>
            <label class="mb-2 block text-sm font-medium text-slate-200">Имя</label>
            <div
              :class="[
                'group relative overflow-hidden rounded-2xl border bg-white/5 transition-all duration-300',
                errors.firstName
                  ? 'border-red-400/60 shadow-[0_0_0_4px_rgba(248,113,113,0.08)]'
                  : 'border-white/10 focus-within:border-cyan-400/50 focus-within:bg-white/10 focus-within:shadow-[0_0_0_4px_rgba(34,211,238,0.08)]'
              ]"
            >
              <div class="pointer-events-none absolute inset-y-0 left-0 flex items-center pl-4 text-slate-400 transition group-focus-within:text-cyan-300">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6.75a3.75 3.75 0 11-7.5 0 3.75 3.75 0 017.5 0zM4.5 19.125a7.5 7.5 0 0115 0" />
                </svg>
              </div>
              <input
                v-model="form.firstName"
                type="text"
                placeholder="Введите имя"
                class="w-full bg-transparent py-4 pl-12 pr-4 text-white placeholder:text-slate-400 outline-none"
              />
            </div>
            <p v-if="errors.firstName" class="mt-2 text-sm text-red-300">
              {{ errors.firstName }}
            </p>
          </div>

          <!-- Фамилия -->
          <div>
            <label class="mb-2 block text-sm font-medium text-slate-200">Фамилия</label>
            <div
              :class="[
                'group relative overflow-hidden rounded-2xl border bg-white/5 transition-all duration-300',
                errors.lastName
                  ? 'border-red-400/60 shadow-[0_0_0_4px_rgba(248,113,113,0.08)]'
                  : 'border-white/10 focus-within:border-fuchsia-400/50 focus-within:bg-white/10 focus-within:shadow-[0_0_0_4px_rgba(217,70,239,0.08)]'
              ]"
            >
              <div class="pointer-events-none absolute inset-y-0 left-0 flex items-center pl-4 text-slate-400 transition group-focus-within:text-fuchsia-300">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6.75a3.75 3.75 0 11-7.5 0 3.75 3.75 0 017.5 0zM4.5 19.125a7.5 7.5 0 0115 0" />
                </svg>
              </div>
              <input
                v-model="form.lastName"
                type="text"
                placeholder="Введите фамилию"
                class="w-full bg-transparent py-4 pl-12 pr-4 text-white placeholder:text-slate-400 outline-none"
              />
            </div>
            <p v-if="errors.lastName" class="mt-2 text-sm text-red-300">
              {{ errors.lastName }}
            </p>
          </div>

          <!-- Телефон -->
          <div>
            <label class="mb-2 block text-sm font-medium text-slate-200">Номер телефона</label>
            <div
              :class="[
                'group relative overflow-hidden rounded-2xl border bg-white/5 transition-all duration-300',
                errors.phone
                  ? 'border-red-400/60 shadow-[0_0_0_4px_rgba(248,113,113,0.08)]'
                  : 'border-white/10 focus-within:border-blue-400/50 focus-within:bg-white/10 focus-within:shadow-[0_0_0_4px_rgba(96,165,250,0.08)]'
              ]"
            >
              <div class="pointer-events-none absolute inset-y-0 left-0 flex items-center pl-4 text-slate-400 transition group-focus-within:text-blue-300">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 4.5c0 9.941 8.059 18 18 18h1.5a2.25 2.25 0 002.25-2.25v-1.372a1.5 1.5 0 00-1.09-1.445l-4.423-1.106a1.5 1.5 0 00-1.584.563l-.97 1.293a1.5 1.5 0 01-1.61.53 14.25 14.25 0 01-8.73-8.73 1.5 1.5 0 01.53-1.61l1.293-.97a1.5 1.5 0 00.563-1.584L6.817 2.84A1.5 1.5 0 005.372 1.75H4A2.25 2.25 0 001.75 4v.5z" />
                </svg>
              </div>
              <input
                v-model="form.phone"
                type="tel"
                placeholder="+998 XX XXX XX XX"
                class="w-full bg-transparent py-4 pl-12 pr-4 text-white placeholder:text-slate-400 outline-none"
              />
            </div>
            <p v-if="errors.phone" class="mt-2 text-sm text-red-300">
              {{ errors.phone }}
            </p>
          </div>

          <!-- Email -->
          <div>
            <label class="mb-2 block text-sm font-medium text-slate-200">Email</label>
            <div
              :class="[
                'group relative overflow-hidden rounded-2xl border bg-white/5 transition-all duration-300',
                errors.email
                  ? 'border-red-400/60 shadow-[0_0_0_4px_rgba(248,113,113,0.08)]'
                  : 'border-white/10 focus-within:border-emerald-400/50 focus-within:bg-white/10 focus-within:shadow-[0_0_0_4px_rgba(52,211,153,0.08)]'
              ]"
            >
              <div class="pointer-events-none absolute inset-y-0 left-0 flex items-center pl-4 text-slate-400 transition group-focus-within:text-emerald-300">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M21.75 7.5v9A2.25 2.25 0 0119.5 18.75h-15A2.25 2.25 0 012.25 16.5v-9m19.5 0A2.25 2.25 0 0019.5 5.25h-15A2.25 2.25 0 002.25 7.5m19.5 0v.243a2.25 2.25 0 01-1.07 1.916l-7.5 4.615a2.25 2.25 0 01-2.36 0L3.32 9.659A2.25 2.25 0 012.25 7.743V7.5" />
                </svg>
              </div>
              <input
                v-model="form.email"
                type="email"
                placeholder="example@mail.com"
                class="w-full bg-transparent py-4 pl-12 pr-4 text-white placeholder:text-slate-400 outline-none"
              />
            </div>
            <p v-if="errors.email" class="mt-2 text-sm text-red-300">
              {{ errors.email }}
            </p>
          </div>

          <button
            type="submit"
            class="relative mt-2 w-full overflow-hidden rounded-2xl bg-gradient-to-r from-cyan-400 via-blue-500 to-fuchsia-500 px-6 py-4 text-base font-bold text-white shadow-[0_10px_30px_rgba(59,130,246,0.35)] transition-all duration-300 hover:-translate-y-1 hover:shadow-[0_20px_40px_rgba(59,130,246,0.45)] active:scale-[0.98]"
          >
            <span class="relative z-10">Отправить заявку</span>
            <span class="absolute inset-0 -translate-x-full skew-x-12 bg-white/20 transition-transform duration-700 hover:translate-x-[180%]"></span>
          </button>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup>
import { reactive, watch } from 'vue'

const form = reactive({
  firstName: '',
  lastName: '',
  phone: '',
  email: '',
})

const errors = reactive({
  firstName: '',
  lastName: '',
  phone: '',
  email: '',
})

const notification = reactive({
  show: false,
  type: 'error',
  message: '',
})

let notificationTimer = null

const showNotification = (type, message) => {
  notification.show = true
  notification.type = type
  notification.message = message

  clearTimeout(notificationTimer)
  notificationTimer = setTimeout(() => {
    notification.show = false
  }, 3500)
}

const validateForm = () => {
  errors.firstName = form.firstName.trim() ? '' : 'Введите имя'
  errors.lastName = form.lastName.trim() ? '' : 'Введите фамилию'
  errors.phone = form.phone.trim() ? '' : 'Введите номер телефона'

  if (!form.email.trim()) {
    errors.email = 'Введите email'
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) {
    errors.email = 'Введите корректный email'
  } else {
    errors.email = ''
  }

  return !errors.firstName && !errors.lastName && !errors.phone && !errors.email
}

const resetForm = () => {
  form.firstName = ''
  form.lastName = ''
  form.phone = ''
  form.email = ''
}

const handleSubmit = () => {
  const isValid = validateForm()

  if (!isValid) {
    showNotification('error', 'Пожалуйста, заполните все поля корректно.')
    return
  }

  console.log('Форма отправлена:', { ...form })

  showNotification('success', 'Спасибо! Ваша заявка успешно отправлена.')
  resetForm()
}

watch(
  () => ({ ...form }),
  () => {
    if (errors.firstName && form.firstName.trim()) errors.firstName = ''
    if (errors.lastName && form.lastName.trim()) errors.lastName = ''
    if (errors.phone && form.phone.trim()) errors.phone = ''
    if (errors.email && /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) errors.email = ''
  },
  { deep: true }
)
</script>

<style scoped>
.form-page {
  position: relative;
  min-height: 100vh;
  width: 100%;
  overflow: hidden;
  background: #020617;
  display: flex;
  align-items: center;
  justify-content: center;
}

.background-layer {
  position: absolute;
  inset: 0;
  overflow: hidden;
}

.overlay-layer {
  position: absolute;
  inset: 0;
  background:
    radial-gradient(circle at top, rgba(255,255,255,0.08), transparent 35%),
    linear-gradient(to bottom, #020617, #0f172a);
}

.grid-layer {
  position: absolute;
  inset: 0;
  opacity: 0.2;
  background-image:
    linear-gradient(rgba(255,255,255,0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.05) 1px, transparent 1px);
  background-size: 40px 40px;
}

.blob {
  position: absolute;
  border-radius: 9999px;
  filter: blur(90px);
  animation: float 10s ease-in-out infinite;
}

.blob-1 {
  top: -80px;
  left: -60px;
  width: 280px;
  height: 280px;
  background: rgba(6, 182, 212, 0.22);
}

.blob-2 {
  top: 25%;
  right: -80px;
  width: 320px;
  height: 320px;
  background: rgba(217, 70, 239, 0.2);
  animation-delay: 1s;
}

.blob-3 {
  bottom: -60px;
  left: 30%;
  width: 260px;
  height: 260px;
  background: rgba(59, 130, 246, 0.18);
  animation-delay: 2s;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0) translateX(0);
  }
  50% {
    transform: translateY(-18px) translateX(12px);
  }
}

@keyframes fadeUp {
  0% {
    opacity: 0;
    transform: translateY(24px) scale(0.98);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.animate-fade-up {
  animation: fadeUp 0.8s ease-out both;
}

.fade-scale-enter-active,
.fade-scale-leave-active {
  transition: all 0.3s ease;
}

.fade-scale-enter-from,
.fade-scale-leave-to {
  opacity: 0;
  transform: translate(-50%, -12px) scale(0.96);
}
</style>
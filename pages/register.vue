<template>
  <div class="container mx-auto w-1/3 py-8">
    <Title>Register | {{ title }}</Title>
    <ul
      v-if="errors.length > 0"
      className="mb-4 list-disc list-inside text-sm text-red-600"
    >
      <li v-for="(error, index) in errors" :key="index">
        {{ error }}
      </li>
    </ul>
    <form action="#" class="space-y-6" @submit.prevent="register">
      <div>
        <label for="name" class="block font-semibold">Name</label>
        <input
          type="text"
          v-model="name"
          id="name"
          class="px-2 py-2 w-full shadow rounded mt-2"
        />
      </div>
      <div>
        <label for="email" class="block font-semibold">Email</label>
        <input
          type="text"
          v-model="email"
          id="email"
          class="px-2 py-2 w-full shadow rounded mt-2"
        />
      </div>
      <div>
        <label for="password" class="block font-semibold">Password</label>
        <input
          type="password"
          v-model="password"
          id="password"
          class="px-2 py-2 w-full shadow rounded mt-2"
        />
      </div>

      <div>
        <label for="passwordConfirm" class="block font-semibold"
          >Password Confirm</label
        >
        <input
          type="password"
          v-model="passwordConfirm"
          id="passwordConfirm"
          class="px-2 py-2 w-full shadow rounded mt-2"
        />
      </div>

      <div>
        <button
          class="inline-block bg-blue-600 hover:bg-blue-700 text-white rounded px-4 py-2"
        >
          Register
        </button>
        <span v-if="isLoading">Loading...</span>
      </div>
    </form>
  </div>
</template>

<script setup>
const title = useState('title')

const router = useRouter()

const name = ref('')
const email = ref('')
const password = ref('')
const passwordConfirm = ref('')
const isLoading = ref(false)
const errors = ref([])

const { $apiFetch } = useNuxtApp()

function csrf() {
  return $apiFetch('/sanctum/csrf-cookie')
}

async function register() {
  await csrf()

  isLoading.value = true

  try {
    await $apiFetch('/register', {
      method: 'POST',
      body: {
        name: name.value,
        email: email.value,
        password: password.value,
        password_confirmation: passwordConfirm.value,
      },
    })

    alert('Registered')
    // router.push('/my-info')
    window.location.pathname = '/my-info'
  } catch (err) {
    console.log(err.data)
    errors.value = Object.values(err.data.errors).flat()
  }

  isLoading.value = false
}
</script>

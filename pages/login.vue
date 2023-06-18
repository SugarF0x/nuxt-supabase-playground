<script setup lang="ts">
import { ref, reactive } from '#imports'

definePageMeta({
  layout: "clear",
})

const supabase = useSupabaseClient()

const email = ref('')
const password = ref('')
const errors = reactive({ email: '', password: '' })

const isLoading = ref(false)
async function submit() {
  isLoading.value = true

  const { data, error } = await supabase.auth.signInWithPassword({ email: email.value, password: password.value })
  console.log({ data, error })

  isLoading.value = false
}

const user = useSupabaseUser()

watchEffect(() => {
  if (user.value) navigateTo('/')
})
</script>

<template>
  <div class="wrapper">
    <v-sheet width="300" class="card">
      <div class="header">
        <h1 class="title text-h2">Вход</h1>
      </div>

      <form @submit.prevent="submit">
        <v-text-field
          v-model="email"
          type="mail"
          label="Почта"
          placeholder="student@mgimo.ru"
          :error-messages="errors.email"
          required
        />

        <v-text-field
          v-model="password"
          type="password"
          label="Пароль"
          :error-messages="errors.password"
          required
        />

        <v-btn type="submit" class="bg-primary" :loading="isLoading">
          Войти
        </v-btn>
      </form>
    </v-sheet>
  </div>
</template>

<style lang="scss" scoped>
.wrapper {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;

  form {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }
}

.header {
  display: flex;
  justify-content: center;
  gap: 16px;
  margin-bottom: 8px;
}

.title {
  margin-bottom: 12px;
  text-align: center;
}

.card {
  padding: 16px;
  border-radius: 16px;
}
</style>

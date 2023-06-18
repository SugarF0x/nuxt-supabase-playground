<script setup lang="ts">
definePageMeta({
  middleware: ['auth']
})

const client = useSupabaseClient()
</script>

<template>
  <h1>i am a protected index page</h1>

  <v-btn @click="client.auth.signOut()">logout</v-btn>
</template>

<style scoped lang="scss">

</style>

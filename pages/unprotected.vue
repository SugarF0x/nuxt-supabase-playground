<script setup lang="ts">
const data = await useFetch('/api/protected-endpoint')
</script>

<template>
  <div>
    <h1>I am an unprotected route</h1>

    <pre>{{ data }}</pre>
  </div>
</template>

<style scoped lang="scss">

</style>

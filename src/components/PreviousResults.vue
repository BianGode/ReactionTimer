<template>
  <div v-for="score in prevScore">
    <h1>
      {{ score }}
    </h1>
  </div>
</template>
<script>
export default {
  data() {
    return {
      prevRes: ['prevScore']
    }
  },
  mounted() {
  }
}
</script>
<style>

</style>
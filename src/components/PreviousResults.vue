<template>
  <div class="prevWrap">
  <h2>Previous scores</h2>
  <div v-if="prevScore" v-for="score in prevRes">
    <h3>
      {{ score }}
    </h3>
  </div>
</div>
</template>
<script>
export default {
  props: ['prevScore'],
  data() {
    return {
      prevRes: this.prevScore
    }
  },
  mounted() {
  }
}
</script>
<style>
.prevWrap {
  width: 100%;
  height: 100%;
}
</style>
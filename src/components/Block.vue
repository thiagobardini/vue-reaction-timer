<template>
  <div class="block" v-if="showBlock">
    click-me
  </div>
</template>

<script>
export default {
  // I want to receive the prop `delay`
  props: ['delay'],
  data() {
    return {
      showBlock: false,
    }
  },
  mounted() {
    setTimeout(() => {
      this.showBlock = true
    }, this.delay)
  },
}
</script>

<style>
.block {
  width: 400px;
  border-radius: 20px;
  background: #0faf87;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>

<template>
  <div>
    <h1>{{ titleHeader }}</h1>
  </div>
</template>

<script>
export default {
  props: {
    titleHeader: {
      type: String,
      required: true/*,
      validator(value) {
        return value.length > 3
      }*/
    }
  }
}
</script>

<style scoped>

</style>
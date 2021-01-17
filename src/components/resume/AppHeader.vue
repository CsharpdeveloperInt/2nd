<template>
  <div>
    <h1>{{ title }}</h1>
  </div>
</template>

<script>
export default {
  props: {
    title: {
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
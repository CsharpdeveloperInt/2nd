<template>
  <p>{{ title }}</p>
</template>

<script>
export default {
  props:{
    title:{
      type: String,
      required: true
    }
  }
}
</script>

<style scoped>

</style>
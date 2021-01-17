<template>
  <div>
    <p><strong>{{ email }}</strong></p>
    <small>{{ textComment }}</small>
  </div>
</template>

<script>
export default {
  props: {
    email:{
      type: String,
      required: true
    },
    textComment:{
      type: String
    }
  }
}
</script>

<style scoped>

</style>
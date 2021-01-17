<template>
    <div class="avatar">
      <img :alt="title" :src="title">
    </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    }
  }
}
</script>

<style scoped>
  .avatar {
    display: flex;
    justify-content: center;
  }
  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
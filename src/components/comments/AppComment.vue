<template>
  <div class="card" v-if="viewComments">
    <h2>Комментарии</h2>
    <ul class="list">
      <li class="list-item" v-for="item in comments">
        <div>
          <p><strong>{{ item.email }}</strong></p>
          <small>{{ item.body }}</small>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props:{
    comments:{
      type: Array,
      required: true
    }
  },
  computed:{
    viewComments(){
      return this.comments.length !== 0
    }
  }
}
</script>

<style scoped>

</style>
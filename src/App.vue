<template>
  <div id="app">
    <div class="container column">
     <AppForm @sub-form="makeComponent"></AppForm>
     <AppResume :components="components"></AppResume>
    </div>
  </div>
  <div class="container">
    <p>
      <button class="btn primary" @click="loadComments">Загрузить комментарии</button>
    </p>
    <AppComment :comments="comments"></AppComment>
    <AppLoader v-if="loading"></AppLoader>
  </div>
</template>

<script>
import AppComment from "@/components/comments/AppComment";
import AppLoader from "@/components/AppLoader";
import AppForm from "@/components/form/AppForm";
import AppResume from "@/components/resume/AppResume";

export default {
  components: {AppComment,AppLoader,AppForm,AppResume},
  data() {
    return {
      components: [],
      comments: [],
      loading: false
    }
  },
  methods: {
    makeComponent(type,val){
      this.components.push({component: type, options: { title: val} })
    },
    async loadComments(){
      try {
        this.loading = true
        const response = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42',{
          method: 'GET',
          headers:{
            'Content-type': 'application/json'
          }
        })
        this.comments = await response.json()
        this.loading = false
      }
      catch (e){
        this.loading = false
        alert('Ошибка: '+e.message)
      }
    }
  }
}
</script>

<style>

</style>

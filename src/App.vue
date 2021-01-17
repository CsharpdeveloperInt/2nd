<template>
  <div id="app">
    <div class="container column">
      <form class="card card-w30" @submit.prevent="makeComponent">
        <div class="form-control">
          <label for="type">Тип блока</label>
          <select id="type" v-model="typeComponent">
            <option value="title">Заголовок</option>
            <option value="subtitle">Подзаголовок</option>
            <option value="avatar">Аватар</option>
            <option value="text">Текст</option>
          </select>
        </div>

        <div class="form-control">
          <label for="value">Значение</label>
          <textarea id="value" rows="3" v-model="valueText"></textarea>
        </div>

        <button class="btn primary" :disabled="viewButton">Добавить</button>
      </form>

      <div class="card card-w70" >
        <h3 v-if="viewCaption">Добавьте первый блок, чтобы увидеть результат</h3>
        <div v-for="item in component">
          <component :is="item.component" v-bind="item.options" ></component>
        </div>
      </div>
    </div>
  </div>
  <div class="container">
    <p>
      <button class="btn primary" @click="loadComments">Загрузить комментарии</button>
    </p>
    <div class="card" v-if="viewComments">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item" v-for="item in comments">
          <AppComment :email="item.email" :text-comment="item.body"></AppComment>
        </li>
      </ul>
    </div>
    <AppLoader v-if="loading"></AppLoader>
  </div>
</template>

<script>
import AppHeader from "@/components/AppHeader";
import AppAvatar from "@/components/AppAvatar";
import AppSubtitle from "@/components/AppSubtitle";
import AppMetaText from "@/components/AppMetaText";
import AppComment from "@/components/AppComment";
import AppLoader from "@/components/AppLoader";

export default {
  components: {AppHeader, AppAvatar, AppSubtitle, AppMetaText,AppComment,AppLoader},
  data() {
    return {
      component: [],
      typeComponent: 'title',
      currentComponent: '',
      valueText: '',
      comments: [],
      loading: false
    }
  },
  methods: {
    makeComponent(){
      if (this.typeComponent === 'title'){
        this.component.push({component: 'AppHeader', options: { titleHeader: this.valueText} })
      }
      if (this.typeComponent === 'subtitle'){
        this.component.push({component: 'AppSubtitle', options: { titleSubtitle: this.valueText} })
      }
      if (this.typeComponent === 'avatar'){
        this.component.push({component: 'AppAvatar', options: { src: this.valueText} })
      }
      if (this.typeComponent === 'text'){
        this.component.push({component: 'AppMetaText', options: { text: this.valueText} })
      }
      this.valueText = ''
      this.typeComponent = 'title'
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
        const result = await response.json()
        this.comments = result
        this.loading = false
      }
      catch (e){
        this.loading = false
        alert('Ошибка: '+e.message)
      }
    }
  },
  computed: {
    viewButton() {
      return this.valueText.length < 3
    },
    viewCaption(){
      return this.component.length === 0
    },
    viewComments(){
      return this.comments.length !== 0
    }
  }
}
</script>

<style>
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

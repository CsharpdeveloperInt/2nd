<template>
  <div class="card card-w70" >
    <h3 v-if="viewCaption">Добавьте первый блок, чтобы увидеть результат</h3>
    <div v-for="item in components">
      <component :is="item.component" v-bind="item.options" ></component>
    </div>
  </div>
</template>

<script>
import AppSubtitle from "@/components/resume/AppSubtitle";
import AppMetaText from "@/components/resume/AppMetaText";
import AppAvatar from "@/components/resume/AppAvatar";
import AppHeader from "@/components/resume/AppHeader";
export default {
  components:{AppSubtitle,AppMetaText,AppAvatar,AppHeader},
  props:{
    components:{
      type: Array,
      required: true
    }
  },
  computed:{
    viewCaption(){
      return this.components.length === 0
    }
  }
}
</script>

<style scoped>

</style>
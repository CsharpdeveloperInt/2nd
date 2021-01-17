<template>
  <form class="card card-w30" @submit.prevent="sendForm">
    <AppSelect v-model="typeSel"></AppSelect>
    <AppInput v-model="val"></AppInput>

    <button class="btn primary" :disabled="viewButton">Добавить</button>
  </form>
</template>

<script>
import AppSelect from "@/components/form/AppSelect";
import AppInput from "@/components/form/AppInput";

export default {
  data(){
    return{
      val: '',
      typeSel: 'AppHeader'
    }
  },
  components:{AppSelect,AppInput},
  emits: ['sub-form'],
  methods:{
    sendForm(){
      this.$emit('sub-form',this.typeSel,this.val)
      this.typeSel = 'AppHeader'
      this.val = ''
    }
  },
  computed:{
    viewButton() {
      return this.val.length < 3
    }
  }
}
</script>

<style scoped>

</style>
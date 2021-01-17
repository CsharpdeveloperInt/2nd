<template>
  <div class="form-control">
    <label for="type">Тип блока</label>
    <select id="type" :value="modelValue" @input="change">
      <option value="AppHeader">Заголовок</option>
      <option value="AppSubtitle">Подзаголовок</option>
      <option value="AppAvatar">Аватар</option>
      <option value="AppMetaText">Текст</option>
    </select>
  </div>
</template>

<script>
export default {
  emits: ['update:modelValue'],
  props:{
    modelValue: String
  },
  methods:{
    change(event){
      this.$emit('update:modelValue',event.target.value)
    }
  }
}
</script>

<style scoped>

</style>
<template>
  <div class="form-control">
    <label for="value">Значение</label>
    <textarea id="value" rows="3" :value="modelValue" @input="change"></textarea>
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
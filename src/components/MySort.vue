<template>
  <span>Сортировка</span>
  <select :value="valueFilter" @change="filterArr">
    <option disabled value="none">Выберете вариант</option>
    <option
      v-for="option in optionsArr"
      :key="option.id"
      :value="option.value"
    >
      {{option.name}}
      {{option.value}}
    </option>
  </select>
</template>

<script>
export default {
  props:{
    optionsArr:{
      type:Array,
      required:true
    },
    valueFilter:{
      type:String,
    }
  },
  methods:{
    filterArr(e){
      this.$emit('update:valueFilter', e.target.value)
    }
  }
}
</script>

<style scoped>

</style>
<template>
  <span>Фильтрация</span>
  <select :value="filterValue" @change="updateFilter">
    <option disabled value="none">Выбор</option>
    <option
    v-for="option in arr"
    :key="option.id"
    :value="option.value"
    >
      {{option.name}}
    </option>
  </select>
</template>

<script>
export default {
  name: "MyFilter",
  props:{
    filterValue:{
      type:String,
      default:''
    },
    arr:{
      type:Array,
    }
  },
  methods:{
    updateFilter(e){
      this.$emit('update:filterValue', e.target.value);
    }
  }
}
</script>

<style scoped>

</style>
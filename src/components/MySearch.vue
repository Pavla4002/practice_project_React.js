<template>
  <div>
   <input class="input" :value="valueSearch" @input="updateValue">
  </div>
</template>

<script>

export default {
  components:{

  },
  props:{
    valueSearch:{
      type:String,
      default:'',
    }
  },
  methods:{
    updateValue(e){
      this.$emit('update:valueSearch',e.target.value);
    },

  }
}
</script>

<style scoped>
.input{
  width: 200px;
  height: 20px;
}
</style>
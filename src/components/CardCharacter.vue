<template>
  <div class="card">
    <span>ID:{{character.id}}</span>
    <span>Name:{{character.name}}</span>
    <span>House:{{character.house}}</span>
  </div>
</template>

<script>
export default {
  props:{
    character:{
      type:Object,
      required:true
    }
  }
}
</script>

<style scoped>
.card{
  width: 90%;
  margin: 10px auto;
  height: 100px;
  display: flex;
  flex-direction: column;
  padding: 15px;
  background-color: yellow;
}
</style>
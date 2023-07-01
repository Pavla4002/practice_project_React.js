<template>
  <div class="cover-all" v-if="show" @click.stop="updateShow">
    <div @click.stop class="slot">
      <slot></slot>
    </div>

  </div>
</template>

<script>
export default {
props:{
  show:{
    type:Boolean,
    default:false
  }
},
  methods:{
    updateShow(){
      this.$emit('update:show',false)
    }
  }
}
</script>

<style scoped>
.cover-all{
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(128, 128, 128, 0.27);
  display: flex;
  justify-content: center;
  align-items: center;
}
.slot{
  width: 30%;
  background-color: #fff;
  display: flex;
  justify-content: center;
}

</style>
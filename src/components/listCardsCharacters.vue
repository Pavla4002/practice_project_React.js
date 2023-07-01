<template>
  <div>
    <card-character v-for="character in characters" :character="character" :key="character.id"/>
  </div>
</template>

<script>
import CardCharacter from "@/components/CardCharacter";
export default {
  components: {CardCharacter},
  props:{
    characters:{
      type:Array,
      required:true
    }
  }
}
</script>

<style scoped>

</style>
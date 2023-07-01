<template>
  <input type="text" placeholder="Введите логин" v-model="userA.email" name="email">
  <label for="login">Введите логин</label>
  <input type="text" placeholder="Введите пароль" v-model="userA.password" name="password" >
  <label for="password">Введите пароль</label>
  <my-button @click="authorizationUser">Авторизоваться</my-button>
</template>

<script>
import MyButton from "@/components/UI/MyButton";
export default {
  name: "AuthorizationUser",
  components: {MyButton},
  data(){
    return{
      userA:{
        password:'',
        email:'',
      }
    }
  },
  methods:{
    authorizationUser(){
      this.$emit('authorization',this.userA)
    }
  }
}
</script>

<style scoped>

</style>
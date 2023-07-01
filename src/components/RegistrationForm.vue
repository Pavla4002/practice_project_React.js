<template>
  <div>
    <div  class="form">
      <input type="text" name="name" id="" placeholder="name" v-model="userInfo.name">
      <input type="text" name="fam" id="" placeholder="fam" v-model="userInfo.fam">
      <input type="text" name="email" id="" placeholder="email" v-model="userInfo.email">
      <input type="text" name="password" id="" placeholder="password" v-model="userInfo.password">
      <div>
        <input  type="radio" name="gen" id="m" v-model="userInfo.gen">
        <label for="m" >М</label>
        <input type="radio" name="gen" id="f" v-model="userInfo.gen">
        <label for="f">Ж</label>
      </div>
      <div>
        <div>
          <input type="checkbox" name="" id="g" v-model="userInfo.interes" value="Grif">
          <label for="g">Гриффендор</label>
        </div>
       <div>
         <input type="checkbox" name="" id="s" v-model="userInfo.interes" value="Sliz">
         <label for="s">Слизарин</label>
       </div>

      </div>
    </div>
    <my-button @click="regUser">Регистрация</my-button>
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton";
export default {
  components:{
    MyButton
  },
  name: "RegistrationForm",
  data(){
   return{
     userInfo:{
      name:'',
       fam:'',
       email:'',
       password:'',
       gen:'',
       interes:[],
     }
   }
  },
  methods:{
    regUser(){
      this.$emit('create',this.userInfo)
    }
  }
}
</script>

<style scoped>
.form{
  width: 300px;
  height: 200px;
  background-color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
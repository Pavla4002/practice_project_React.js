<template>
  <div class="main">
    <my-sort :options-arr="options" v-model:value-filter="valueSort"/>
    <my-filter :arr="filterOptions" v-model:filter-value="valueFilter"/>
    <my-text>{{valueSearch}} Да</my-text>
    <my-search v-model:value-search="valueSearch" @create="action"/>
    <my-button @click="openModalW">Регистрация</my-button>
    <my-button @click="openModalAutho">Авторизация</my-button>
    <list-cards-characters :characters="filterArr"/>
    <model-window v-model:show="openAutho" >
      <authorization-user @authorization="userAutho"/>
    </model-window>
    <model-window v-model:show="openModal" >
      <registration-form @create="regUser"/>
    </model-window>
  </div>
</template>

<script>
import ListCardsCharacters from "@/components/listCardsCharacters";
import MyButton from "@/components/UI/MyButton";
import ModelWindow from "@/components/UI/ModelWindow";
import MySearch from "@/components/MySearch";
import MyText from "@/components/UI/MyText";
import MyFilter from "@/components/MyFilter";
import MySort from "@/components/MySort";
import RegistrationForm from "@/components/RegistrationForm";
import AuthorizationUser from "@/components/AuthorizationUser";

export default {
  components: {
    AuthorizationUser,
    RegistrationForm, MySort, MyFilter, MyText, MySearch, ModelWindow, MyButton, ListCardsCharacters},
  data(){
    return{
      arrUsers:[],
      user:[],
      statusUser:false,
      mas:[],
      searchArr:[],
      openModal:false,
      openAutho:false,
      valueSearch:'',
      valueFilter:'none',
      valueSort:'none',
      options:[
        {value:"name",name:"По возростанию"},
        {value:"nameY",name:"По убыванию"},
      ],
      filterOptions:[
        {value:"Gryffindor", name:"Gryffindor"},
        {value:"Slytherin", name:"Slytherin"},
        {value:"Ravenclaw", name:"Ravenclaw"},
      ]
    }
  },
  methods:{
    async loadCard(){
      let response = await fetch('https://hp-api.onrender.com/api/characters');
      let data = await response.json();
      this.arrUsers=data;
    },
    openModalW(){
      this.openModal = true;
    },
    openModalAutho(){
      this.openAutho = true;
    },
    updateShow(){
      this.openModal = false;
    },
    regUser(userInfo){
      console.log(userInfo)
      let key = Date.now();
      console.log(userInfo);
      this.openModal = false;
      localStorage.setItem(key.toString(),JSON.stringify(userInfo));
    },
    userAutho(userA){
      console.log(userA)
      for(let i =0; i<localStorage.length;i++){
        let key = localStorage.key(i);
        let value = localStorage[key];
        let user1 = JSON.parse(value)
        console.log(key)
        if((userA.email===user1.email) && (userA.password===user1.password)){
         this.user.push(userA)
        }
      }
      console.log(userA)
      console.log(this.user)
      if(this.user.length>0){
        this.statusUser=true;
        alert('Вы успешно авторизованы');
        this.openAutho=false;
      }else{
        this.openAutho=false;
        this.openModal=true
      }
    }

  },
  computed:{
    sortArr(){
      console.log(this.valueSort);
      switch (this.valueSort){
        case "name":
          return [...this.arrUsers].sort((p,q) => (p["name"]?.localeCompare(q["name"]) ));
        case "nameY":
          return [...this.arrUsers].sort((p,q) => -1 * (p["nameY"]?.localeCompare(q["nameY"]) ));
        default :
          return [...this.arrUsers].sort((p,q) => p[this.valueSort]?.localeCompare(q[this.valueSort]));
      }
    },
    action(){
        return this.sortArr.filter(post =>((post.name.toLowerCase()).includes(this.valueSearch.toLowerCase())));

    },
    filterArr(){
      if(this.valueFilter!=='none'){
        return [...this.action.filter(home => home.house===this.valueFilter)]
      }else{
        return this.action
      }

    }
  },
  mounted() {
    this.loadCard()
  }
}
</script>

<style scoped>

</style>

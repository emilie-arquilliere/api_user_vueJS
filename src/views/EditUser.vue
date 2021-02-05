<template>
  <h1>Edit User n° {{`${this.$route.params.id}`}}</h1>
  <br>
  <div>
    <button class="btn btn-primary" @click="back">Retour</button>
  </div>
  <InputText label="Nom" :value="user.lastName" ref="lastName" :changeInput="changeInput" />
  <br>
  <InputText label="Prénom" :value="user.firstName" ref="firstName" :changeInput="changeInput" />
  <br>
  <!--<InputText label="Email" :value="user.email" />
  <br>
  <InputText label="Anniversaire" :value="user.birthDate" />
  <br>
  <RadioButton :id="user.id" :user="user"/>-->
  <br>
  <SaveButton :id="user.id" :user="user"/>

</template>

<script>
import InputText from "../components/formulaire/InputText.vue"
import SaveButton from "../components/formulaire/SaveButton.vue"
//import RadioButton from "../components/formulaire/RadioButton.vue"
import axios from "axios"

export default {
  name: 'EditUser',
  components: {
    InputText,
    SaveButton,
   // RadioButton
  },
  data(){
    return{
      user: {}
    }
  },
  methods:{
    back(){
      this.$router.go(-1);
    },
    fetchUser(){
      axios
      .get(`http://localhost:6929/users/${this.$route.params.id}`)
      .then(response => this.user = response.data)
    },
    changeInput(){
      this.user.lastName = this.$refs.lastName.val
      this.user.firstName = this.$refs.firstName.val
    }
  },
  created(){this.fetchUser();}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.headt{
  display: flex;
  justify-content: space-around;
}
.btn-primary{
  background-color: #41B883!important;
  border-color: #41B883!important;
}
.btn-primary:hover{
  background-color: #35495E!important;
}
</style>
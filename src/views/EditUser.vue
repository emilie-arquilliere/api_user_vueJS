<template>
  <h1>Edit User n° {{`${this.$route.params.id}`}}</h1>
  <br><br>
  <div>
    <button class="btn btn-primary" @click="back">Retour</button>
     <ResetButton :id="user.id" :user="user" :resetForm="resetForm" />
  </div>
  <br>
  <div>
    <img :src="user.avatarUrl" class="img" />
    <InputFile label="Choisir une photo" :id="user.id" ref="avatarUrl" :changeInput="changeInput" />
  </div> 
  <div>
    <InputText label="Nom" :value="user.lastName" ref="lastName" :changeInput="changeInput" />
    <InputText label="Prénom" :value="user.firstName" ref="firstName" :changeInput="changeInput" />
  </div>

  <br>
  <InputText label="Email" :value="user.email" ref="email" :changeInput="changeInput" />
  <br>
  <InputDate label="Anniversaire" :value="user.birthDate" ref="birthDate" :changeInput="changeInput" />
  <br>
  <GenderRadio :value="user.gender" ref="gender" :changeInput="changeInput" />
  <br>
  <SaveButton :id="user.id" :user="user" />

</template>

<script>
import InputFile from "../components/formulaire/InputFile.vue"
import InputText from "../components/formulaire/InputText.vue"
import InputDate from "../components/formulaire/InputDate.vue"
import SaveButton from "../components/formulaire/SaveButton.vue"
import GenderRadio from "../components/formulaire/GenderRadio.vue"
import ResetButton from "../components/formulaire/ResetButton.vue"
import axios from "axios"

export default {
  name: 'EditUser',
  components: {
    InputFile,
    InputText,
    InputDate,
    SaveButton,
    GenderRadio,
    ResetButton
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
      .then(response => this.user = response.data )
    },
    changeInput(){
      this.user.avatarUrl = this.$refs.avatarUrl.file
      this.user.lastName = this.$refs.lastName.val
      this.user.firstName = this.$refs.firstName.val
      this.user.email = this.$refs.email.val
      this.user.birthDate = this.$refs.birthDate.val
      this.user.gender = this.$refs.gender.radioValue
    },
    resetForm(){
      this.user = {}
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
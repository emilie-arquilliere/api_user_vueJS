<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <h1>Fetch Users with VueJS</h1>
  <br>
  <button class="btn btn-primary" v-on:click="fetchUsers">FetchUsers</button>
  <label> 
    <input type="checkbox" v-model="genderFilter" value="male" />
    Fetch male
  </label>
  <label>
    <input type="checkbox" v-model="genderFilter" value="female" />
    Fetch female
  </label>
  <br>
  <label>
    Search : 
    <input type="search" v-model="search" />
  </label>
  <TakeUser :usersFiltered="usersFiltered" />
</template>

<script>
import TakeUser from './components/TakeUser.vue'
import axios from "axios"

export default {
  name: 'App',
  components: {
    TakeUser
  },
  data(){
    return{
      users: [],
      genderFilter: ['male', 'female'],
      search : ''
    }
  },
  computed:{
    usersFiltered(){
      return this.users
                .filter(
                  (user) => {
                    let filter = new RegExp(this.search, "i");
                    this.genderFilter.includes(user.gender);
                    user.name.last.match(filter);
                    user.name.first.match(filter);
                    user.email.match(filter);
                  }
                )
    }
  },
  methods:{
   async fetchUsers(){
      await axios
      .get("https://randomuser.me/api/?results=20")
      .then(response => this.users = this.users.concat(response.data.results))
    }
  }
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
</style>

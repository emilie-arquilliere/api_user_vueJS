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
  <span>Nombre d'utilisateur : {{usersFiltered.length}}</span>
  <br>
  <label>
    Search : 
    <input type="search" v-model="search" />
  </label>
  <TakeUser :usersFiltered="usersFiltered" :sortDirection="sortDirection" :sort="sort" />
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
      search: '',
      sortDirection : 'asc',
      sortKey : 'dob.age'
    }
  },
  computed:{
    usersFiltered(){
      const filter = new RegExp(this.search, "i");
      return this.users
                  .filter( (user) => (this.genderFilter.includes(user.gender)) )
                  .filter( user => user.name.last.match(filter) || user.name.first.match(filter) )
                  .sort( (u1,u2) => {
                    const modifier = this.sortDirection === 'desc' ? -1 : 1;
                    return (u1.dob.age - u2.dob.age) * modifier;
                  })
    } 
  }, 
  methods:{
    fetchUsers(){
       axios
      .get("https://randomuser.me/api/?results=20")
      .then(response => this.users = this.users.concat(response.data.results))
    },
    sort(key){
      if(this.sortKey === key) {
          this.sortDirection = this.sortDirection === 'asc' ? 'desc' : 'asc';
      }
    }
  },
  beforeMount(){
    this.fetchUsers();
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

<template>
  <h1>Fetch Users with VueJS</h1>
  <br>
   <div class="headt">
    <button class="btn btn-primary" v-on:click="fetchUsers">Récupérer des utilisateurs</button>
    <label>
      <input v-model="genderFilter" type="checkbox" value="male" :disabled="genderFilter.length<2 && genderFilter.includes('male')" />
      Hommes
    </label>
    <label>
      <input v-model="genderFilter" type="checkbox" value="female" :disabled="genderFilter.length<2 && genderFilter.includes('female')"/>
      Femmes
    </label>
    <label>
      Rechercher :
      <input type="search" v-model="search" placeholder="Rechercher"/>
    </label>  
    <button class="btn btn-primary" @click="resetFilter">Reset</button>
    <label>
      Trier par âge :
      <p v-if="sortDirection === ''">Par défaut</p>
      <p v-if="sortDirection === 'asc'">Croissant</p>
      <p v-if="sortDirection === 'desc'">Décroissant</p>
    </label>
    <button class="btn btn-primary" v-on:click="openModal">Créer un utilisateur</button>
    <Modal v-show="isModalVisible" @close="closeModal"/>
  </div>
  
  <p v-if="usersFiltered.length">Il y a <strong>{{usersFiltered.length}}</strong> utilisateurs sur {{users.length}}</p>
  <p v-else >Il y a <strong>0</strong> utilisateur sur {{users.length}}</p>
  <TakeUser :usersFiltered="usersFiltered" :sortDirection="sortDirection" :changeSort="changeSort" />
</template>

<script>
import TakeUser from '../components/TakeUser.vue'
import Modal from '../components/Modal.vue'
import axios from "axios"

export default {
  name: 'App',
  components: {
    TakeUser,
    Modal
  },
  data(){
    return{
      users: [],
      genderFilter: (this.$route.query.gender || 'male,female').split(","),
      search: this.$route.query.search || '',
      sortDirection : this.$route.query.sortAge || '',
      isModalVisible: false
    }
  },
  computed:{
    usersFiltered(){
      const filter = new RegExp(this.search, "i");
      return this.users
                  .filter( user => this.genderFilter.includes(user.gender) )
                  .filter( user => user.lastName.match(filter) || user.firstName.match(filter) )
                  .sort( (u1,u2) => {
                    if (!this.sortDirection) return 0;
                    const  modifier = this.sortDirection === 'desc' ? -1 : 1;
                    return (u1.age - u2.age) * modifier;
                  })
    } 
  }, 
  methods:{
    fetchUsers(){
       axios
      .get("http://localhost:6929/users")
      .then(response => this.users = this.users.concat(response.data))
    },
    updateQuery(){
      const query = {}
      if(this.genderFilter.length < 2){
        query.gender = this.genderFilter.join(',')
      }
      if(this.search){
        query.search = this.search
      }
      if(this.sortDirection){
        query.sortAge = this.sortDirection
      }
      this.$router.push({ query })
    },
    changeSort(){
      if(this.sortDirection === ''){
        this.sortDirection = 'asc'
      }else if(this.sortDirection ==='asc'){
        this.sortDirection = 'desc'
      }else if(this.sortDirection === 'desc'){
        this.sortDirection = ''
      }
    },
    resetFilter(){
      this.genderFilter = ['male', 'female'];
      this.search = '';
      this.sortDirection = '';
    },
    openModal(){
      this.isModalVisible = true
    },
    closeModal(){
      this.isModalVisible = false
    }
  },
  watch:{
    search(){
      this.updateQuery();
    },
    sortDirection(){
      this.updateQuery();
    },
    genderFilter(){
      this.updateQuery();
    }    
  },
  created(){this.fetchUsers();}
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
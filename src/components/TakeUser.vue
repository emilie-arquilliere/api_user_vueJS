<template>
  <div class="hello">
    <table id="tbl-users" class="table table-hover" v-if="usersFiltered.length">
      <thead>
        <tr>
          <th></th>
          <th></th>
          <th></th>
          <th>Nom</th>
          <th>Prénom</th>
          <th>Email</th>
          <th @click="changeSort">
            Âge
            <i v-if="sortDirection" class="fa" v-bind:class="[ sortDirection === 'asc' ? 'fa-sort-up' : 'fa-sort-down' ]"></i>
          </th>
          <th>Genre</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in usersFiltered" :key="user">
          <td>
            <router-link :to="{name : 'EditUser', params: {id: user.id} }">
              <img src="https://cdn.pixabay.com/photo/2016/11/01/03/28/magnifier-1787362_1280.png" class="logo_img" />
            </router-link>
          </td>
          <td><img src="https://img.icons8.com/color/452/recycle-bin.png" @click="deleteUser(user.id)" class="logo_img" /></td>
          <td><img :src="user.avatarUrl" class="img" /></td>
          <td>{{user.lastName}} </td>
          <td>{{user.firstName}}</td>
          <td>{{user.email}}</td>
          <td>{{user.age}}</td>
          <td v-if="user.gender === 'male'">M</td>
          <td v-else>F</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'TakeUser',
  props: {
    usersFiltered: Array,
    genderFilter : Array,
    search : String,
    sortDirection : String,
    changeSort : Function
  },
  methods: {
    deleteUser(id){
      if(confirm("Êtes vous sûr de vouloir supprimer cet utilisateur ?")){
        axios
        .delete(`http://localhost:6929/user/`+id)
        .then(()=>{
          alert("L'utilisateur a bien été supprimé !");
          this.$router.go(-1);
        });
      }
    }
  },
  watch:{
    changeSort(){
      this.$parent.changeSort()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.logo_img{
  width:50px;
  height:auto;
}
</style>

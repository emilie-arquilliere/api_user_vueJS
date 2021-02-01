<template>
  <div class="hello">
    <table id="tbl-users" class="table table-hover">
      <thead>
        <tr>
          <th></th>
          <th>Nom</th>
          <th>Prénom</th>
          <th>Email</th>
          <th @click="sort('dob.age')" :class="[sortKey === 'dob.age' ? sortDirection : '']">Age
            <img src="https://image.flaticon.com/icons/png/512/36/36687.png" width="15" v-if="sortDirection=='asc'" />
            <img src="http://cdn.onlinewebfonts.com/svg/img_339653.png" width="15" v-else />
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in usersFiltered" :key="user">
          <td><img :src="user.picture.thumbnail"/></td>
          <td>{{user.name.last}}</td>
          <td>{{user.name.first}}</td>
          <td>{{user.email}}</td>
          <td>{{user.dob.age}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'TakeUser',
  props: {
    usersFiltered: Array,
    genderFilter : Array,
    search : String,
    sortDirection : String,
    sortKey : String,
    sort : Function
  },
  mounted(){
    this.$parent.sort();
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
</style>

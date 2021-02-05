<template>
    <button v-if="id" @click="editUser(`http://localhost:6929/users/${this.id}`)" class="btn btn-primary">Save 1</button>
    <button v-else @click="editUser(`http://localhost:6929/users`)">Save 2</button>
</template>

<script>
import axios from 'axios'

export default{
    name: 'SaveButton',
    props:{
        id: String,
        user: Object
    },
    methods:{
        editUser(url){
            axios
            .put(url, this.user)
            .then(()=>{
                alert('ok 1');
                this.$router.go(-1);
            });
        }
    }
}
</script>
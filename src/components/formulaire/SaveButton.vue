<template>
    <button v-if="id" @click="testData(`http://localhost:6929/users/${this.id}`)" class="btn btn-primary">Save 1</button>
    <button v-else @click="testData(`http://localhost:6929/users`)">Save 2</button>
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
                alert('Utilisateur enregistré');
                this.$router.go(-1);
            });
        },
        testData(url){
            const reg = new RegExp(/([a-zA-Z0-9_.]+@[a-zA-Z_\-.]+\.[a-zA-Z]{2,})/i)
            let msg = ''
            let ok = 1
            if(!reg.test(this.user.email)){
                msg += "L'adresse email n'est pas valide"
                ok = 0
            }
            
            if(ok === 0) alert(msg)
            else this.editUser(url)
        }
    }
}
</script>
<template>
    <button v-if="id" @click="testData(1)" class="btn btn-primary">Enregistrer</button>
    <button v-else @click="testData(2)" class="btn btn-primary">Enregistrer</button>
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
        editUser(rqt){
            if(rqt===1){
                axios
                .put(`http://localhost:6929/users/${this.id}`, this.user)
                .then(()=>{
                    alert('Utilisateur enregistré');
                    this.$router.go(-1);
                });
            }else{
                axios
                .post(`http://localhost:6929/users`, this.user)
                .then(()=>{
                    alert('Utilisateur enregistré');
                    this.$router.go(-1);
                });
            }
        },
        testData(rqt){
            const regEmail = new RegExp(/([a-zA-Z0-9_.]+@[a-zA-Z_\-.]+\.[a-zA-Z]{2,})/i)
            const regDate = new RegExp(/([0-9]{4}-[0-9]{2}-[0-9]{2})/i)
            let msg = ''
            let ok = 1
            if(!regEmail.test(this.user.email)){
                msg += "L'adresse email n'est pas valide\n"
                ok = 0
            }
            if(!regDate.test(this.user.birthDate)){
                msg += "La date d'anniversaire doit être au format AAAA-MM-JJ\n"
                ok = 0
            }
            if(this.user.gender !== "male" && this.user.gender!== "female"){
                msg += "Le genre n'est pas sélectionné\n"
                ok = 0
            }

            if(ok === 0) alert(msg)
            else this.editUser(rqt)
        }
    }
}
</script>
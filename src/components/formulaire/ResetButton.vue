<template>
    <button @click="resetUser" class="btn btn-primary">Reset</button>
</template>

<script>
export default{
    name: 'ResetButton',
    props:{
        id: String,
        user: Object,
        resetForm: Function
    },
    data(){
        return{
            resUser: {}
        }
    },
    methods:{
        resetUser(){
            this.$parent.resetForm()
        }
    },
    watch:{
        user(){
            this.resUser = this.user
        }
    }
}
</script>
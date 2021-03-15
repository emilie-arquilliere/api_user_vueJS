<template>
    <label>
        {{label}}
        <input type="text" v-model="val" class="form-control">
    </label>
    
</template>

<script>
export default{
    name: 'InputText',
    props:{
        label: String,
        value: String,
        changeInput: Function
    },
    data(){
        return{
            val: ''
        }
    },
    watch:{
        value(){
            this.val = this.value
        },
        val(){
            this.$parent.changeInput();
        }
    }
}
</script>
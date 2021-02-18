<template>
    <label>
        {{label}}
        <input type="date" v-model="val">
    </label>
    
</template>

<script>
export default{
    name: 'InputDate',
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
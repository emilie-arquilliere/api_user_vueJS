<template>
    <label>
        URL photo
        <input type="text" v-model="val" class="form-control">
    </label>
</template>

<script>
export default{
    name: 'InputFile',
    props:{
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
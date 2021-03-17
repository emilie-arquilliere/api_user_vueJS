<template>
    <label for="female">
        <input type="radio" value="female" v-model="radioValue" name="gender" id="female" />
        Femme
    </label>
    <br>
    <label for="male">
        <input type="radio" value="male" v-model="radioValue" name="gender" id="male" />
        Homme
    </label>
</template>

<script>
export default{
    name: 'GenderRadio',
    props:{
        value: String,
        changeInput: Function
    },
    data(){
        return{
            radioValue: ''
        }
    },
    watch:{
        value(){
            this.radioValue = this.value
        },
        radioValue(){
            this.$parent.changeInput();
        }
    }
}
</script>
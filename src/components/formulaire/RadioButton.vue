<template>
    <label>
        Femme
        <input type="radio" value="female" />
    </label>
    <label>
        Homme
        <input type="radio" value="male" />
    </label>
    
</template>

<script>
export default{
    name: 'RadioButton',
    props:{
        value: String
    }
}
</script>
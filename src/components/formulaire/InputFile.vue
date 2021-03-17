<template>
    <label>
        {{label}}
        <input id="file_id" class="form-control" type="file" @change="changeFile($event)"/>
    </label>
</template>

<script>
export default{
    name: 'InputFile',
    props:{
        label: String,
        id: String,
        changeInput: Function
    },
    data(){
        return{
            file: ''
        }
    },
    methods:{
        changeFile(event) {
            this.file = event.target.files[0];
            this.$parent.changeInput();
        }
    }
}
</script>
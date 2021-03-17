<template>
  <div class="modal-backdrop">
    <div class="modal">
      <header class="modal-header">
        <h1 name="header">
          Create a new user !
        </h1>
        <button type="button" class="btn-close" @click="close">x</button>
      </header>
      <section class="modal-body">
        <ResetButton :id="user.id" :user="user" :resetForm="resetForm" />
        <br>
        <div>
          <img :src="user.avatarUrl" class="img" />
          <InputFile label="Choisir une photo" :id="user.id" ref="avatarUrl" :changeInput="changeInput" />
        </div>
        <div>
          <InputText label="Nom" :value="user.lastName" ref="lastName" :changeInput="changeInput" />
          <InputText label="Prénom" :value="user.firstName" ref="firstName" :changeInput="changeInput" />
        </div>
        <InputText label="Email" :value="user.email" ref="email" :changeInput="changeInput" />
        <br>
        <InputDate label="Anniversaire" :value="user.birthDate" ref="birthDate" :changeInput="changeInput" />
        <br>
        <GenderRadio :value="user.gender" ref="gender" :changeInput="changeInput" />
       </section>
       <footer class="modal-footer">
          <SaveButton :id="user.id" :user="user" />
      </footer>
    </div>
  </div>
</template>

<script>
import InputFile from "../components/formulaire/InputFile.vue"
import InputText from "../components/formulaire/InputText.vue"
import InputDate from "../components/formulaire/InputDate.vue"
import SaveButton from "../components/formulaire/SaveButton.vue"
import GenderRadio from "../components/formulaire/GenderRadio.vue"
import ResetButton from "../components/formulaire/ResetButton.vue"

export default{
    name: 'Modal',
    components: {
        InputFile,
        InputText,
        InputDate,
        SaveButton,
        GenderRadio,
        ResetButton
    },
    data(){
        return{
            user: {}
        }
    },
    methods: {
      close() {
        this.$emit('close');
      },
      changeInput(){
        this.user.avatarUrl = this.$refs.avatarUrl.file
        this.user.lastName = this.$refs.lastName.val
        this.user.firstName = this.$refs.firstName.val
        this.user.email = this.$refs.email.val
        this.user.birthDate = this.$refs.birthDate.val
        this.user.gender = this.$refs.gender.radioValue
      },
      resetForm(){
        this.user = {}
      }
    },
    watch:{
        user(){
            this.resUser = this.user
        }
    }
}
</script>

<style>
.modal-backdrop {
    position: fixed;
    top: 25%;
    bottom: 25%;
    left: 25%;
    right: 25%;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: #FFFFFF;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
  }

  .modal-header,
  .modal-footer {
    padding: 15px;
    display: flex;
    margin-left:auto;
    margin-right:auto;
  }

  .modal-header {
    border-bottom: 1px solid #eeeeee;
    color: #4AAE9B;
    justify-content: space-between;
  }

  .modal-footer {
    border-top: 1px solid #eeeeee;
    justify-content: flex-end;
  }

  .modal-body {
    position: relative;
    padding: 20px 10px;
  }

  .btn-close {
    border: none;
    font-size: 20px;
    padding: 20px;
    cursor: pointer;
    font-weight: bold;
    color: #4AAE9B;
    background: transparent;
  }
</style>
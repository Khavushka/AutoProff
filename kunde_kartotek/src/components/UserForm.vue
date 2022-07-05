<template>
        <form @submit.prevent>
          <h4>Tilføje medarbejder</h4>
          <select
            v-model="user.company"
            placeholder="Afdeling">
              <option v-for="company in companys">{{ company }}</option>
            </select>
          <my-input 
            v-model="user.name"
            class="input" 
            type="text" 
            placeholder="Navn"/>
          <my-input 
            v-model="user.title"
            class="input" 
            type="text" 
            placeholder="Title"/>
          <my-input 
            v-model="user.phone"
            class="input" 
            type="phone" 
            name="tel"
            placeholder="Telefonnr."/>
          <my-button style="align-self: flex-end; margin-top: 15px;" @click="createUser" >Opret</my-button>
      </form>
</template>
    
<script>
import UserItem from "./UserItem.vue"

export default {
  components: {
    UserItem
  },
  data(){
    return {
      user: {
        company: '',
        name: '',
        title: '',
        phone: ''
      },
      companys:['Syd', 'Vest', 'Øst']
    }
  },
  methods: {
    createUser() {
      this.user.id = Date.now();
      this.$emit('create', this.user)
      this.user = {
        company: '',
        name: '',
        title: '',
        phone: ''
      }
    }
  }
}
</script>

<style>
form {
  display: flex;
  flex-direction: column;
}
</style>
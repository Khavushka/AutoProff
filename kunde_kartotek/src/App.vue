<template>
  <div class="app" id="app">
    <div class="users">
      <h1>Medarbejderkartotek</h1>
      <my-input v-model="searchQuery" placeholder="Search..."/>
      <div class="app__btns">
        <my-button @click="showDialog">Opret medarbejder</my-button>
        <my-select
          v-model="selectedSort"
          :options="sortOptions"
        />
      </div>
      <my-dialog  v-model:show="dialogVisible">
        <user-form
          @create="createUser"/>
      </my-dialog>
  
        <user-list 
          :users="sortedAndSearchedUsers"
          @remove="removeUser"
          v-if="!isUsersLoading"
          />
          <div v-else>Loading ...</div>
    </div>
  </div>
</template>

<script> 
import UserForm from "./components/UserForm.vue";
import UserList from "./components/UserList.vue";
import MyButton from "./components/UI/MyButton.vue";
import MyInput from "./components/UI/MyInput.vue";
import axios from 'axios';
import MySelect from "./components/UI/MySelect.vue"
import MyCh from "./components/UI/MyCh.vue"


export default {
  components: {
    MyInput, MyButton, 
    UserList, UserForm 
  },
  data() {
    return {
      users: [],
      dialogVisible: false,
      isUsersLoading: false,
      selectedSort:'',
      searchQuery: '',
      sortOptions: [
        {value: 'company',  name: 'Afdeling'},
        {value: 'name',  name: 'Navn'},
        {value: 'phone',  name: 'Telefonnr.'},
      ]
    }
  },
  mounted(){
    // this.fetchUsers();
    if (localStorage.users){
      this.users  = JSON.parse(localStorage.users);
    }
  },
  watch: {
    users: {
      handler(newUser){
      localStorage.users = JSON.stringify(newUser);
      },
      deep: true
    }
  },
  methods: {
    createUser(user) {
        this.users.push(user);
        this.dialogVisible = false;
    },
    removeUser(user) {
      this.users = this.users.filter(p => p.id !== user.id)
    },
    showDialog() {
      this.dialogVisible = true;
    },
    // async fetchUsers() {
    //   try{
    //     this.isUsersLoading = true;
    //       const response = await axios.get('https://jsonplaceholder.typicode.com/users');
    //       this.users = response.data;
    //   } catch (e) {
    //       alert('Oops, mistake')
    //   } finally {
    //     this.isUsersLoading = false;
    //   }
    // }
  },
  computed:{
    sortedUsers() {
      return [...this.users].sort((user1, user2, user3) => user1[this.selectedSort]?.localeCompare(user2[this.selectedSort]))
    },
    sortedAndSearchedUsers(){
      return this.sortedUsers.filter(user => user.name.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}

.app__btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}

</style>
<template>
  <div class="home">
    <div class="container">
      <Button
        title="Добавить"
        :click="toggleModal"
      />
      <div class="table-wrpr" v-if="users.length">
        <Table :users="users"/>
      </div>
    </div>

    <AddUserModal
      v-if="openModal"
      :close="toggleModal"
      :users="users"
      :add="addUser"
    />
  </div>
</template>

<script>
import Button from '@/components/Base/Button';
import Table from '@/components/Base/Table';
import AddUserModal from '@/components/Modal/AddUserModal';

export default {
  name: 'Home',
  components: {
    Button,
    Table,
    AddUserModal,
  },
  data () {
    return {
      openModal: false,
      users: [],
    }
  },
  methods:{
    toggleModal(){
      this.openModal = !this.openModal;
    },
    addUser(newUser){
      console.log('newUser:', newUser);
      
      this.openModal = false;
      this.users.push(newUser);

      localStorage.setItem('vue-test-user', JSON.stringify(this.users));
    },
  },
  created(){
    let storageUsers = localStorage.getItem('vue-test-user');
    if(storageUsers){
      this.users = JSON.parse(storageUsers);
    }
  }
}
</script>

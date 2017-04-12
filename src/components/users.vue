<template>
  <div class="users">
    <h1>Users</h1>
    <input type="text" v-model="newUser.name" placeholder="Enter Name">
    <br />
    <input type="text" v-model="newUser.email" placeholder="Enter Email">
    <br />
    <button v-on:click="addUser()">Add User</button>
    <ul>
      <li v-for="user in users">
        <input type="checkbox" class="toggle" v-model="user.contacted">
        <span :class="{contacted: user.contacted}">
        {{user.name}} | {{user.email}} <button v-on:click="deleteUser(user)">x</button>
        </span>
      </li>

    </ul>
  </div>
</template>

<script>
  export default {
    name: 'users',
    data() {
      return {
        newUser: {},
        users: [ ]
      }
    },
    methods: {
      addUser: function(){
        this.users.push({
          name: this.newUser.name,
          email: this.newUser.email,
          contacted: false
        });
      },
      deleteUser: function(user){
        this.users.splice(this.users.indexOf(user),1);
      }
    },
    created: function(){
      this.$http.get('https://jsonplaceholder.typicode.com/users')
        .then(function(response){
          this.users = response.data;
        });
    }
  }
</script>

<style scoped>
  .users{
    text-align: left;
  }
  ul{
    list-style-type: none;
  }
  .contacted{
    text-decoration: line-through;
  }
</style>

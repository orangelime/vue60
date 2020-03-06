<template>
  <div class="users">
    <h1>Users</h1>
    <form v-on:submit="addUser">
      <input type="text" v-model="newUsers.name" placeholder="Enter Name">
      <br/>
      <input type="text" v-model="newUsers.email" placeholder="Enter E-mail">
      <br/>
      <input type="submit" value="Submit">
    </form>
    <ul>
      <li v-for="user in users">
        <input type="checkbox" class="toggle" v-model="user.contacted">
        <span :class="{contacted: user.contacted}">
          {{user.name}}: {{user.email}} <button v-on:click="deleteUser(user)">x</button>
        </span>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name:'users',

  data(){
    return{
      newUsers:{},
      users:[]
        /*{
          name:'John Doe',
          email:'jdoe@gmail.com',
          contacted:false
        },
        {
          name:'Steve Smith',
          email:'ssmith@gmail.com',
          contacted:false
        },
        {
          name:'Tim White',
          email:'tomwhite@gmail.com',
          contacted:false
        }
        */


    }
  },
  methods:{
    addUser:function(e){
      this.users.push({
        name:this.newUsers.name,
        email:this.newUsers.email,
        contacted:false
      });
      e.preventDefault();
    },
    deleteUser:function(user){
      this.users.splice(this.users.indexOf(user),1);
    }
  },
  created:function(){
    /*console.log("creat run...");*/
    this.$http.get('https://jsonplaceholder.typicode.com/users')
    .then(function(response){
      /*console.log(response.data);*/
      this.users = response.data;
    });
  }
}
</script>
<style scoped>
  .contacted{
    text-decoration: line-through;
  }
</style>


<template>
    <div id="appp" class="small-container">
     
      <!-- <img id="image" src="./assets/logo.png" alt="VueJS" /> -->
      <h1>User Register</h1>
      <user-form  @add:user="addUser" />
  
      <!-- <br/><br/>
      <hr/>
      <br/>
      <h1>User Details</h1>
      <user-details v-bind:users ="users"
      @edit:employee="editEmployee"
                        @delete:employee="deleteEmployee"
      /> -->
    </div>
  <!-- <template>
    <div id="nav">
      <router-link to="/">Register</router-link> |
      <router-link to="/details">details</router-link>
    </div>
    <router-view/>
  
  
  </template> -->
    </template>
  
  
  
  
  <script>
  import userForm from '../components/userForm.vue';
//   import userDetails from './components/userDetails.vue';
  export default {
    name: 'appp',
    components: {
      userForm
    },
    data() {
      return {
        users: [],
      }
    },
    methods: {
      async addUser(employee) {
        try {
          const response = await fetch('http://localhost:3080/account/addaccount', {
            method: 'POST',
            body: JSON.stringify(employee),
            headers: { "Content-type": "application/json; charset=UTF-8" }
          });
          const data = await response.json()
          
          this.users = [...this.users, data]
        } catch (error) {
          console.error('Error occured while adding employee: ' +error)
        }
        window.location.reload();
      },
      
    },
    // mounted() {
    //   this.getEmployees()
    // }
    
    }
  </script>
  
  <style>
     #appp {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  } 
 
  /* #nav {
    padding: 30px;
  }
  
  #nav a {
    font-weight: bold;
    color: #2c3e50;
  }
  
  #nav a.router-link-exact-active {
    color: #42b983;
  } */
  button {
    background: #41b883;
    border: 1px solid #41b883;
  }
  .small-container {
    max-width: 720px;
     font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: left;
    color: #2c3e50;
    margin-top: 10px;
    margin-left: 10px;
  }
  </style>
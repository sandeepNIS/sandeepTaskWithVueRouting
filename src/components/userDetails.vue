
<template>
    <div id="user-details" className="table-wrapper table-responsive table-responsive{-sm|-md|-lg|-xl}   overflow-x:auto;">
      <p v-if="users.length < 1">
        No users
      </p>
      <table v-else className="table table-success table-responsive{-sm|-md|-lg|-xl} table-bordered striped bordered table-hover"  responsive size="sm" w-auto="true">
        <thead>
          <tr>
            <th>Name</th>
            <th>Email</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" v-bind:key="user.id">
            <td v-if="editing === user.id">
              <input type="text" v-model="user.username" />
            </td>
            <td v-else>{{ user.username }}</td>
  
            <td v-if="editing === user.id">
              <input type="text" v-model="user.email" />
            </td>
            <td v-else>{{ user.email }}</td>
  
            <td v-if="editing === user.id">
              <button @click="editUser(user)">Save</button>
              <button @click="cancelEdit(user)" class="muted-button">Cancel</button>
            </td>
  
            <td v-else>
              <button @click="editMode(user)">Edit</button>
              <button @click="$emit('delete:user', user.id)" class="delete-button">Delete</button>
            </td>
  
          </tr>
        </tbody>
      </table>
    </div>
  </template>
    
  <script>
import 'bootstrap/dist/css/bootstrap.css';   
    export default {
      name: 'user-details',
      props: {
        users: Array,
      },
      data() {
        return {
          editing: null,
        }
      },
      methods: {
        editMode(users) {
          this.cachedUser = Object.assign({}, users)
          this.editing = users.id
        },
        cancelEdit(user) {
          Object.assign(user, this.cachedUser)
          this.editing = null
        },
        editUser(user){
          if(user.username === '' || user.email === '') return
          this.$emit('edit:user', user.id, user)
          this.editing = null        
        },
      }
    }
  </script>
  
  <style scoped>
  
  button {
    margin: 0 0.5rem 0 0;
  }
  input {
    margin: 0;
  }
  .empty-table {
    text-align: center;
  }

  @media screen and (max-width: 400px) {
  table {
    border: 0;
  } 

  
  
   table thead {
    border: none;
    clip: rect(0 0 0 0);
    height: 1px;
    margin: -1px;
    overflow: hidden;
    padding: 0;
    position: absolute;
    width: 1px;
  }
  
  thead tr {
      position: absolute;
      top: -9999px;
      left: -9999px;
    }

  table tr {
    border-bottom: 3px solid #ddd;
    display: block;
    margin-bottom: .625em;
  }
  
  
  

  table td {
    border-bottom: 1px solid #ddd;
    display: block;
    font-size: .9em;
    text-align: center;
  }
  
  table td::before {
   
    content: attr(data-label);
    float: left;
    font-weight: bold;
    text-transform: uppercase;
  }
  
  table td:last-child {
    border-bottom: 0;
  } 
  td:nth-of-type(1):before { content: "Name "; }
  td:nth-of-type(2):before { content: "Email "; }
  td:nth-of-type(3):before { content: "Action "; }
} 
  </style>
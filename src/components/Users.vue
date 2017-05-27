<template>
  <div class="test" >
    <div class="alert alert-danger alert-manteinance" role="alert">This app will be in mantainance sunday 8 a.m to 10 p.m EST</div>
    <h1>Users</h1>
    <input type="text" v-model="newUser.name" placeholder="Enter name..." /><br>
    <input type="text" v-model="newUser.email" placeholder="Enter name..." /><br>
    <input type="submit" value="Add user" v-on:click="addUser" /> 
    <ul>
      <li v-for="user in users" >
        <input type="checkbox" class="toggle" v-model="user.contacted" />
        <span :class="{ contacted: user.contacted }">
          {{user.name}}: {{user.email}}
        </span>
        <input type="button" value="X" v-on:click="deleteUser(user)" />
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'users',
    data () {
      return {
        users: [],
        newUser: {}
      }
    },
    methods: {
      addUser: function (e) {
        console.log('saving user...')
        if (this.newUser.name !== undefined && this.newUser.email !== undefined) {
          this.users.push({
            name: this.newUser.name,
            email: this.newUser.email,
            contacted: false
          })
        }
        e.preventDefault()
      },
      deleteUser: function (user) {
        this.users.splice(this.users.indexOf(user), 1)
      }
    },
    created: function () {
      this.$http.get('https://jsonplaceholder.typicode.com/users', { params: {} })
      .then(function (response) {
        this.users = response.data
      })
    }
  }
</script>

<style lang="scss" >
  .contacted {
    text-decoration: line-through;
  }
  .alert-manteinance {
    margin-top: 60px;
  }
</style>

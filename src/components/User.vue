<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <div class="card">
          <div class="card-header">Vue Axios Post - ItSolutionStuff.com</div>

          <div class="card-body">
            <form @submit="formSubmit">
              <strong>Name:</strong>
              <input type="text" class="form-control" v-model="username">
              <strong>Description:</strong>
              <textarea class="form-control" v-model="email"></textarea>
              <strong>firstname:</strong>
              <input type="text" class="form-control" v-model="firstname">
              <strong>lastname:</strong>
              <input type="text" class="form-control" v-model="lastname">
              <strong>password:</strong>
              <input type="password" class="form-control" v-model="password">
              <strong>id_role:</strong>
              <input type="text" class="form-control" v-model="id_role">

              <button class="btn btn-success">Submit</button>
            </form>
          </div>
        </div>
        <button  v-on:click="created">GET</button>
        <p> {{email}} ------------ {{username}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'User',
  mounted () {
    console.log('Component mounted.')
  },
  data () {
    return {
      username: '',
      email: '',
      password: '',
      firstname: '',
      lastname: '',
      id_role: ''
    }
  },
  methods: {
    created: function (event) {
      this.axios.get(`http://localhost:3000/users/3`)
        .then(response => {
          // JSON responses are automatically parsed.
          this.username = response.data.username
          this.email = response.data.email
          console.log(response)
          console.log(response.data.username)
          console.log(this.email + '------' + this.username)
        })
        .catch(e => {
          this.errors.push(e)
        })
    },
    formSubmit (e) {
      e.preventDefault()
      let currentObj = this
      this.axios.post('http://localhost:3000/users/', {
        username: currentObj.username,
        email: currentObj.email,
        password: currentObj.password,
        firstname: currentObj.firstname,
        lastname: currentObj.lastname,
        id_role: currentObj.id_role

      })
        .then(function (response) {
          console.log(response.user)
          currentObj.output = response.user
        })
        .catch(function (error) {
          console.log(currentObj.username)
          console.log(error)
          currentObj.output = error
        })
    }
  }
  /* methods: {
    createUser: function () {
      this.ajaxRequest = true
      this.$http.post('http://localhost:4000/api/users', {
        username: this.username,
        email: this.email
      }, function (data, status, request) {
        this.postResults = data

        this.ajaxRequest = false
      })
    }
  } */
}
</script>

<style scoped>

</style>

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

              <button class="btn btn-success">Submit</button>
            </form>
            <strong>Output:</strong>
            <pre>
                        {{output}}
                        </pre>
          </div>
        </div>
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
      output: ''
    }
  },
  methods: {
    formSubmit (e) {
      e.preventDefault()
      let currentObj = this
      this.axios.post('http://localhost:4000/api/users', {
        username: this.username,
        email: this.email,
        useCredentails: true
      })
        .then(function (response) {
          currentObj.output = response.data
        })
        .catch(function (error) {
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

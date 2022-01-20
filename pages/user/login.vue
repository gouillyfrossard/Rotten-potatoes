<template>
  <div class="mx-5">
    <h1 class="text-center text-white pt-5">Login</h1>
   

    <div class="row pt-5"> 
    <div class="alert alert-success" v-if="$route.params.registered == 'yes'">
      You have registered successfully
    </div>

    <form
      class="form-wrapper"
      action=""
      method="post"
      @submit.prevent="submitForm()"
    >
      <div class="form-group">
        <label for="" class="text-white">Email</label>
        <input
          type="text"
          class="form-control"
          :class="{ 'is-invalid': errors && errors.email }"
          v-model="email"
        />
        <div class="invalid-feedback" v-if="errors && errors.email">
          {{ errors.email.msg }}
        </div>
      </div>

      <div class="form-group">
        <label for="" class="text-white">Password</label>
        <input
          type="password"
          class="form-control"
          :class="{ 'is-invalid': errors && errors.password }"
          v-model="password"
        />
        <div class="invalid-feedback" v-if="errors && errors.password">
          {{ errors.password.msg }}
        </div>
      </div>

      <div class="alert alert-danger" v-if="login_error">
        {{ login_error }}
      </div>
      <div class="text-center mt-20">
        <input type="submit" value="Login" class="btn btn-danger" />
        <nuxt-link to="/" class="btn btn-secondary ml-3">Cancel</nuxt-link>
      </div>
    </form>
    </div>  
  </div>
</template>

<script>
export default {
  middleware: 'auth',
  auth: 'guest',
  data() {
    return {
      errors: null,
      login_error: null,
      email: null,
      password: null,
      status: false,
    }
  },

  methods: {
    submitForm() {
      this.$auth
        .loginWith('local', {
          data: {
            email: this.email,
            password: this.password,
          },
        })
        .then((response) => {
          this.$auth.setUser(response.data.user)
          console.log(response.data.user) // this data is ok
        })
        // this.$auth.loginWith('local', {
        // data: {
        // email: this.email,
        // password: this.password}
        // })
        // .then(() => this.$toast.success('Logged In!'))

        .catch((error) => {
          console.log(error)
          if (error.response.data.message) {
            this.login_error = error.response.data.message
          }
        })
    },
  },
}
</script>

<style scoped>
.form-wrapper {
  width: 70% !important;
  max-width: 40em !important;
  margin: 0 auto !important;
}
@media only screen and (max-width: 466px) {
  .form-wrapper {
    width: 90% !important;
  }
}

</style>
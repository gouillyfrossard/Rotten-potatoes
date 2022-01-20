<template>
  <div class="mx-5">
    <h1 class="text-center text-white pt-5">My Account</h1>


    <div class="card text-white bg-secondary">
      <div class="card-body">
        <h4>{{ this.$auth.user.full_name }}</h4>
        <div class="mb-5">
          <strong>Email:</strong> {{ this.$auth.user.email }}
        </div>
        <router-link
          :to="{ name: 'user-edit', params: { id: this.$auth.user._id } }"
          class="btn btn-danger"
          >Edit</router-link>

        <nuxt-link to="/user/logout" class="btn btn-secondary">Logout</nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  middleware: 'auth',
}
</script>

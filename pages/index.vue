<template>
  <div class="w-screen">
    <navbar></navbar>
    <div class="login-form flex justify-center">
      <div class="div w-1/3 my-10 bg-green-100 p-10">
        Login
        <hr class="my-4">
        <div class="form">
          <Form>
            <div class="form-group flex flex-col my-1">
              <label>Username</label>
              <input class="p-2 rounded-md" type="text" name="username" id="" required>
            </div>
            <div class="form-group flex flex-col my-1">
              <label>password</label>
              <input class="p-2 rounded-md" type="password" name="username" id="" required>
            </div>
            <div class="button flex justify-center">
              <button @click.prevent="$router.push({name: 'booking'})" type="submit" class="bg-green-600 px-4 py-2 mt-2">Login</button>
            </div>
          </Form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import navbar from '../components/Nav.vue';
export default {
  data() {
    return {
      
    }
  },
  components: {
    navbar,
  },
  mounted() {
  },
  methods: {
    
  }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
</style>

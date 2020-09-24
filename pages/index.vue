<template>
  <div class="container">
    <div class="card mt-4">
      <div class="card-header bg-light">
        <h1 class="title">Login</h1>
      </div>
      <div class="card-body">
        <form>
          <div class="mb-3">
            <label for="email">email</label>
            <input
              id="email"
              v-model.trim="$v.form.email.$model"
              type="text"
              class="form-control"
            />
          </div>
          <div class="mb-3">
            <label for="password">password</label>
            <input
              id="password"
              v-model="$v.form.password.$model"
              type="text"
              :class="[
                { 'is-invalid': $v.form.password.$error },
                'form-control',
              ]"
            />
            <div class="invalid-feedback">This field is required</div>
          </div>
          <p class="text-center">
            <button class="btn btn-primary">Se connecter</button>
          </p>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import { required, email } from 'vuelidate/lib/validators'

export default {
  data() {
    return {
      form: {
        email: '',
        password: '',
      },
    }
  },
  validations: {
    form: {
      email: {
        required,
        email,
      },
      password: {
        required,
      },
    },
  },
}
</script>
<style>
.title {
  font-family: 'Rancho', cursive;
  font-size: 4rem;
  text-align: center;
}
</style>

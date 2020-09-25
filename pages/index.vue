<template>
  <div class="container">
    <div class="card mt-4">
      <div class="card-header bg-light">
        <h1 class="title">Login</h1>
      </div>
      <div class="card-body">
        <form @submit.prevent="onSubmit">
          <div class="mb-3">
            <label for="email">email</label>
            <input
              id="email"
              v-model.trim="$v.form.email.$model"
              type="text"
              :class="[{ 'is-invalid': $v.form.email.$error }, 'form-control']"
            />
            <div
              v-if="submitted && !$v.form.email.$error"
              class="invalid-feedback"
            >
              <span v-if="!$v.form.email.required">Email is required</span>
              <span v-if="!$v.form.email.email">Email is invalid</span>
            </div>
          </div>
          <div class="mb-3">
            <label for="password">password</label>
            <input
              id="password"
              v-model="$v.form.password.$model"
              type="password"
              :class="[
                { 'is-invalid': $v.form.password.$error },
                'form-control',
              ]"
            />
            <div
              v-if="submitted && !$v.form.password.required"
              class="invalid-feedback"
            >
              Password is required
            </div>
          </div>
          <p class="text-center">
            <button type="submit" class="btn btn-primary">Se connecter</button>
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
      submitted: false,
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
  methods: {
    async onSubmit() {
      this.submitted = true
      // stop here if form is invalid
      this.$v.$touch()
      if (this.$v.$invalid) {
        this.submitted = false
        return
      }
      const result = await this.$axios.$post(
        'http://localhost:5000/api/v1/auth/login',
        this.form
      )

      alert('SUCCESS!! :-)\n\n' + JSON.stringify(result))
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

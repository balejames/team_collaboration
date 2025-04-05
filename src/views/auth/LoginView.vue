<script setup>
import { ref } from 'vue'

const email = ref('')
const password = ref('')
const barangay = ref('')
const role = ref('')

const emailError = ref('')
const passwordError = ref('')
const barangayError = ref('')

const roles = ref(['Viewer', 'Barangay'])

const submit = () => {
  let valid = true

  // Email Validation
  if (!validateEmail(email.value)) {
    emailError.value = 'Please enter a valid email address.'
    valid = false
  } else {
    emailError.value = ''
  }

  // Password Validation
  if (!password.value) {
    passwordError.value = 'Password is required.'
    valid = false
  } else {
    passwordError.value = ''
  }

  // Barangay Validation
  if (!barangay.value) {
    barangayError.value = 'Barangay is required.'
    valid = false
  } else {
    barangayError.value = ''
  }

  // If all fields are valid
  if (valid) {
    alert(`Submitted: ${email.value}, Role: ${role.value}`)
  }
}

const validateEmail = (email) => {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
}
</script>
<template>
  <div class="login-wrapper">
    <v-container>
      <v-row justify="center" align="center">
        <v-col cols="6"
          ><p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Perferendis in quod incidunt
            nostrum dolores est reprehenderit quasi illum accusamus alias, voluptates fuga adipisci
            voluptatem natus doloremque velit? Accusamus, harum saepe.
          </p></v-col
        >
        <v-col cols="6" md="4" class="mx-auto">
          <v-card class="mx-auto">
            <template v-slot:title>
              <h2 class="text-center">Log In</h2>
            </template>
            <v-card-text>
              <v-form fast-fail @submit.prevent>
                <v-text-field
                  v-model="email"
                  label="Email"
                  required
                  type="email"
                  :error-messages="emailError"
                  variant="outlined"
                ></v-text-field>
                <v-text-field
                  v-model="password"
                  label="Password"
                  required
                  type="password"
                  :error-messages="passwordError"
                  variant="outlined"
                ></v-text-field>
                <v-text-field
                  v-model="barangay"
                  label="Barangay"
                  required
                  type="text"
                  :error-messages="barangayError"
                  variant="outlined"
                ></v-text-field>
                <v-select
                  v-model="role"
                  :items="roles"
                  :rules="[(v) => !!v || 'Role is required']"
                  s
                  label="Role"
                  required
                  variant="outlined"
                ></v-select>
                <v-btn
                  type="submit"
                  style="background-color: #0dceda; color: white"
                  class="custom-login my-2 mx-auto d-block"
                  >Log In</v-btn
                >
                <v-divider class="my-5"></v-divider>
                <h4 class="text-center">
                  Don't have an account? <RouterLink to="/register">Sign up!</RouterLink>
                </h4>
              </v-form>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<style>
.login-wrapper {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.custom-login {
  height: 50px;
  width: 150px;
  font-size: 16px;
  border-radius: 8px;
}
.v-card {
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  border-radius: 12px;
  background-color: #ebfffa;
}
body {
  background-color: #c6fce5;
}
</style>

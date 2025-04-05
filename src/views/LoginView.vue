<template>
  <v-card class="mx-auto my-8" elevation="16" max-width="344">
    <v-card-item>
      <div class="d-flex justify-center mb-6">
        <h1><b>LOG IN</b></h1>
      </div>

      <form @submit.prevent="submit">
        <v-text-field
          v-model="email"
          label="Email"
          required
          type="email"
          :error-messages="emailError"
        ></v-text-field>

        <v-text-field
          v-model="password"
          label="Password"
          required
          type="password"
          :error-messages="passwordError"
        ></v-text-field>

        <v-text-field
          v-model="barangay"
          label="Barangay"
          required
          type="text"
          :error-messages="barangayError"
        ></v-text-field>

        <v-select
          v-model="role"
          :items="roles"
          :rules="[(v) => !!v || 'Role is required']"
          label="Role"
          required
        ></v-select>

        <v-btn type="submit" color="primary" block class="mt-4">Log In</v-btn>
      </form>
    </v-card-item>
  </v-card>
</template>

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

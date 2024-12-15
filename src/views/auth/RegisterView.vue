<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const theme = ref('light')
const router = useRouter()

function toggleTheme() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

const name = ref('')
const email = ref('')
const password = ref('')
const confirmPassword = ref('')

const nameRules = [(v) => !!v || 'Name is required']
const emailRules = [(v) => !!v || 'E-mail is required']
const passwordRules = [(v) => !!v || 'Password is required']
const confirmPasswordRules = [
  (v) => !!v || 'Confirm Password is required',
  (v) => v === password.value || 'Passwords must match',
]

function handleBackToLogin() {
  router.push({ name: 'login' })
}

function handleRegister() {
  if (name.value && email.value && password.value && confirmPassword.value === password.value) {
    alert('Registration successful!')
    router.push({ name: 'login' })
  } else {
    alert('Please fill in all required fields correctly.')
  }
}
</script>

<template>
  <v-responsive class="border rounded">
    <v-app :theme="theme">
      <!-- App Bar -->
      <v-app-bar class="px-3" elevation="3">
        <span class="text-h6 font-weight-medium">CooKify</span>
        <v-spacer></v-spacer>
        <v-btn
          :prepend-icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'"
          text="Toggle Theme"
          @click="toggleTheme"
        ></v-btn>
      </v-app-bar>

      <!-- Main Content -->
      <v-main>
        <v-container>
          <v-row justify="center">
            <v-col cols="12" sm="8" md="6">
              <!-- Card Section -->
              <v-card
                class="mx-auto text-center"
                width="400"
                :class="[theme === 'light' ? 'bg-surface-light' : 'bg-surface-dark']"
                elevation="15"
              >
                <template v-slot:title>
                  <h2 class="text-h5 font-weight-bold">Create an Account</h2>
                </template>

                <v-card-text class="py-3">
                  Join CooKify today and discover the joy of cooking with personalized recipes and
                  expert tips. Sign up now!
                </v-card-text>
              </v-card>

              <!-- Registration Form -->
              <v-form fast-fail @submit.prevent="handleRegister">
                <v-text-field
                  v-model="name"
                  :rules="nameRules"
                  label="First Name"
                  variant="outlined"
                  clearable
                  outlined
                  class="mt-4"
                ></v-text-field>

                <v-text-field
                  v-model="name"
                  :rules="nameRules"
                  label="Last Name"
                  variant="outlined"
                  clearable
                  outlined
                  class="mt-4"
                ></v-text-field>

                <v-text-field
                  v-model="email"
                  :rules="emailRules"
                  label="E-mail"
                  type="email"
                  variant="outlined"
                  clearable
                  outlined
                  class="mt-4"
                ></v-text-field>

                <v-text-field
                  v-model="password"
                  :rules="passwordRules"
                  label="Password"
                  type="password"
                  variant="outlined"
                  clearable
                  outlined
                  class="mt-4"
                ></v-text-field>

                <v-text-field
                  v-model="confirmPassword"
                  :rules="confirmPasswordRules"
                  label="Confirm Password"
                  type="password"
                  variant="outlined"
                  clearable
                  outlined
                  class="mt-4"
                ></v-text-field>

                <v-btn class="mt-4" type="submit" block color="primary" elevation="2">
                  Register
                </v-btn>

                <!-- Back to Login Button -->
                <v-btn class="mt-2" text block color="secondary" @click="handleBackToLogin">
                  Already have an account? Login here.
                </v-btn>
              </v-form>
            </v-col>
          </v-row>
        </v-container>
      </v-main>

      <!-- Footer -->
      <v-footer
        app
        elevation="2"
        class="text-center py-2"
        :class="[theme === 'light' ? 'bg-surface-light' : 'bg-surface-dark']"
      >
        <span>© 2024 CooKify. All rights reserved.</span>
      </v-footer>
    </v-app>
  </v-responsive>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const theme = ref('light')
const router = useRouter()

function toggleTheme() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

const email = ref('')
const password = ref('')
const emailRules = [
  (v) => !!v || 'E-mail is required',
  (v) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(v) || 'E-mail must be valid',
]
const passwordRules = [(v) => !!v || 'Password is required']

const validCredentials = {
  email: 'test@codebuddy.com',
  password: 'password123',
}

function handleLogin() {
  if (email.value && password.value) {
    if (email.value === validCredentials.email && password.value === validCredentials.password) {
      alert('Login successful! Welcome to CodeBuddy!')

      router.push({ name: 'home' })
    } else {
      alert('Invalid email or password. Please try again.')
    }
  } else {
    alert('Please fill in all required fields.')
  }
}

function handleRegisterRedirect() {
  router.push({ name: 'register' })
}
</script>

<template>
  <v-responsive
    class="border rounded"
    style="
      background: url('public/img/467457975_540707448765983_2165938018579944350_n.png') no-repeat
        center center / cover;
      height: 100vh;
    "
  >
    <v-app :theme="theme">
      <!-- App Bar -->
      <v-app-bar class="px-3" elevation="3">
        <span class="text-h6 font-weight-medium">Codebuddy</span>
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
                  <h2 class="text-h5 font-weight-bold">Welcome to Codebuddy!</h2>
                </template>

                <v-card-text class="py-3">
                  Discover and create delicious meals effortlessly with our detailed recipes,
                  step-by-step instructions, and expert tips. Sign in now to start your culinary
                  journey!
                </v-card-text>
              </v-card>

              <!-- Login Form -->
              <v-form fast-fail @submit.prevent="handleLogin">
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

                <v-btn class="mt-4" type="submit" block color="primary" elevation="2">
                  Login
                </v-btn>

                <!-- Register Button -->
                <v-btn class="mt-2" text block color="secondary" @click="handleRegisterRedirect">
                  Don't have an account? Register here.
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

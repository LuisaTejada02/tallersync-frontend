<template>
  <div class="login-page">
    <div class="login-card">
      <h1>TallerSync</h1>
      <p class="subtitle">Sistema de Gestión de Talleres</p>

      <input
        v-model="email"
        type="email"
        placeholder="Correo electrónico"
      />

      <input
        v-model="password"
        type="password"
        placeholder="Contraseña"
      />

      <button @click="login">
        Iniciar Sesión
      </button>
      <p class="register-link">
  ¿No tienes cuenta?
  <router-link to="/register">
    Regístrate aquí
  </router-link>
</p>

      <p class="message">{{ mensaje }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router'

const router = useRouter()

const email = ref('')
const password = ref('')
const mensaje = ref('')

const login = async () => {
  try {
    const response = await axios.post(
      'http://localhost:3000/api/auth/login',
      {
        email: email.value,
        password: password.value
      }
    )

    localStorage.setItem(
      'token',
      response.data.data.token
    )

    router.push('/dashboard')

  } catch (error) {
    mensaje.value = 'Correo o contraseña incorrectos'
  }
}
</script>

<style scoped>
.register-link {
  text-align: center;
  margin-top: 15px;
}

.register-link a {
  color: #2563eb;
  text-decoration: none;
  font-weight: bold;
}

.register-link a:hover {
  text-decoration: underline;
}
.login-page {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #f8fafc;
}

.login-card {
  width: 400px;
  background: white;
  padding: 40px;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.1);
}

h1 {
  text-align: center;
  color: #040f2c;
  margin-bottom: 10px;
}

.subtitle {
  text-align: center;
  color: gray;
  margin-bottom: 25px;
}

input {
  width: 100%;
  padding: 12px;
  margin-bottom: 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-sizing: border-box;
}

button {
  width: 100%;
  padding: 12px;
  border: none;
  border-radius: 8px;
  background: #821029;
  color: white;
  font-weight: bold;
  cursor: pointer;
}

button:hover {
  background: #5b0a11;
}

.message {
  margin-top: 15px;
  text-align: center;
  color: red;
}
</style>
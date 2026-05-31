<template>
  <div class="register-page">
    <div class="register-card">
      <h1>Crear Cuenta</h1>


      <input v-model="full_name" placeholder="Nombre completo" />

      <input
        v-model="email"
        type="email"
        placeholder="Correo electrónico"
      />

      <input
        v-model="phone"
        placeholder="Teléfono"
      />

    <select v-model="role">
  <option value="client">Cliente</option>
  <option value="admin">Administrador</option>
</select>
      <input
        v-model="password"
        type="password"
        placeholder="Contraseña"
      />

      <button @click="register">
        Registrarse
      </button>

      <p>{{ mensaje }}</p>

      <router-link to="/login">
        Volver al login
      </router-link>
    </div>
  </div>
</template>

<script setup>

const role = ref('client')
import { ref } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router'

const router = useRouter()

const full_name = ref('')
const email = ref('')
const phone = ref('')
const password = ref('')
const mensaje = ref('')

const register = async () => {
  try {
    await axios.post(
      'http://localhost:3000/api/auth/register',
      {
        full_name: full_name.value,
        email: email.value,
        phone: phone.value,
        password: password.value,
        role: role.value
      }
    )

    mensaje.value = 'Usuario registrado'

    setTimeout(() => {
      router.push('/login')
    }, 1500)

  } catch (error) {
    console.error(error)
    mensaje.value = 'Error al registrar'
  }
}
</script>

<style scoped>
select {
  width: 100%;
  padding: 12px;
  margin-bottom: 12px;
  box-sizing: border-box;
  border: 1px solid #ddd;
  border-radius: 8px;
}
.register-page {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #f8fafc;
}

.register-card {
  width: 420px;
  background: white;
  padding: 40px;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0,0,0,.1);
}

input {
  width: 100%;
  padding: 12px;
  margin-bottom: 12px;
  box-sizing: border-box;
}

button {
  width: 100%;
  padding: 12px;
  border: none;
  background: #2563eb;
  color: white;
  border-radius: 8px;
  cursor: pointer;
}
</style>
<template>
  <div class="login-page">
    <div class="login-card">
     <div class="logo">
 <img
  src="/logo.png"
  alt="TallerSync"
  class="logo-img"
/>
</div>

<p class="subtitle">
  Bienvenido, ingresa tus credenciales
</p>

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
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');

*{
  font-family:'Poppins',sans-serif;
}
.login-page {
  min-height: 100vh;

  display: flex;
  justify-content: center;
  align-items: center;

  background-image:
    linear-gradient(
      rgba(5, 10, 25, 0.65),
      rgba(5, 10, 25, 0.65)
    ),
    url('/fondo-login.png');

  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
.login-card {
  width: 420px;

  background: rgba(2, 20, 50, 0.758);

  backdrop-filter: blur(10px);

  border: 1px solid #8B1E1E;

  border-radius: 20px;

  padding: 40px;

  box-shadow:
    0 0 20px rgba(212,175,55,.2);
}
.logo-img{
  width: 320px;
  display: block;
  margin: 0 auto 2px auto;
}
input{
  width:100%;
  padding:14px;

  background:transparent ;

  border:1px solid #3b4a63;

  border-radius:10px;

  color:white;

  margin-bottom:15px;
}
label{
  color:white;
  font-weight:600;
  font-size:16px;
}
button{
  width: 220px;

  display: block;

  margin: 20px auto;

  padding: 14px;

  background:#8B1E1E;
  color:black;

  border:none;
  border-radius:10px;

  font-weight:600;
  cursor:pointer;
}
.subtitle{
  color:#d1d5db;
  text-align:center;
  font-size:18px;
  font-weight:400;
  margin-bottom:30px;
}

.message{
  text-align:center;
  color:#8B1E1E;
  margin-top:15px;
}

.register-link{
  text-align:center;
  margin-top:20px;
  color:rgb(84, 79, 79);
}

.register-link a{
  color:#8B1E1E;
  text-decoration:none;
  font-weight:bold;
}

.register-link a:hover{
  text-decoration:underline;
}

input::placeholder{
  color:#9ca3af;
}
</style>
<template>
  <div class="register-page">
    <div class="register-card">
        <img
  src="/logo.png"
  alt="TallerSync"
  class="logo-img"
/>

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
        Volver a Inicio de Sesión
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
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');

*{
  font-family:'Poppins',sans-serif;
}
.logo-img{
  width:260px;
  display:block;
  margin:0 auto 15px auto;
}
.register-page{
  min-height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;

  background-image:
    linear-gradient(
      rgba(5,10,25,.70),
      rgba(5,10,25,.70)
    ),
    url('/fondo-login.png');

  background-size:cover;
  background-position:center;
}

.register-card{
  width:450px;

  background:rgba(5,15,35,.88);

  backdrop-filter:blur(10px);

  border:1px solid #8B1E1E;

  border-radius:25px;

  padding:40px;

  box-shadow:
    0 0 25px rgba(139,30,30,.25);
}

.register-card h1{
  text-align:center;
  color:white;
  margin-bottom:25px;
}

input,
select{
  width:100%;
  padding:14px;

  background:#0f172a;

  color:white;

  border:1px solid #8B1E1E;

  border-radius:10px;
}

option{
  background:#0f172a;
  color:white;
}

input::placeholder{
  color:#94a3b8;
}

select{
  cursor:pointer;
}

button{
  width:100%;

  padding:14px;

  border:none;

  border-radius:10px;

  background:#8B1E1E;

  color:white;

  font-weight:600;

  cursor:pointer;

  transition:.3s;
}

button:hover{
  background:#a32424;
}

p{
  text-align:center;
  margin-top:15px;
  color:white;
}

a{
  display:block;
  text-align:center;
  margin-top:15px;
  color:#ffffff;
  text-decoration:none;
  font-weight:600;
}

a:hover{
  color:#8B1E1E;
}
</style>
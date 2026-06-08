<template>
    <div class="dashboard">

<aside
  class="sidebar">

    <div class="sidebar-header">
  <img
    src="/logo.png"
    class="sidebar-logo"
  />

  <div class="sidebar-user">

    <h4>{{ userName }}</h4>

    <span>
      {{ role === 'admin'
        ? 'Administrador'
        : 'Cliente' }}
    </span>

  </div>

</div>

        <ul class="menu">
           <li class="menu-item">
  Inicio
</li>

<li
  class="menu-item"
  v-if="role === 'admin'"
>
  Usuarios
</li>

<li
  class="menu-item"
  v-if="role === 'client'"
>
  Mi Perfil
</li>

          <li
            class="menu-item"
            @click="vehiculosOpen = !vehiculosOpen"
          >
            {{ vehiculosOpen ? '▼' : '▶' }}
            Vehículos
          </li>
          

          <ul
            v-if="vehiculosOpen"
            class="submenu"
          >
            <li>Ver Vehículos</li>
            <li>Registrar Vehículo</li>
          </ul>

          <li
            class="menu-item"
            @click="citasOpen = !citasOpen"
          >
            {{ citasOpen ? '▼' : '▶' }}
            Citas
          </li>

          <ul
            v-if="citasOpen"
            class="submenu"
          >
            <li>Ver Citas</li>
            <li>Agendar Cita</li>
          </ul>

          <li
            class="menu-item"
            @click="cotizacionesOpen = !cotizacionesOpen"
          >
            {{ cotizacionesOpen ? '▼' : '▶' }}
            Cotizaciones
          </li>

          <ul
            v-if="cotizacionesOpen"
            class="submenu"
          >
            <li>Ver Cotizaciones</li>
            <li>Nueva Cotización</li>
          </ul>

          <li
            class="menu-item"
            @click="ordenesOpen = !ordenesOpen"
          >
            {{ ordenesOpen ? '▼' : '▶' }}
            Órdenes
          </li>

          <ul
            v-if="ordenesOpen"
            class="submenu"
          >
            <li>Ver Órdenes</li>
            <li>Nueva Orden</li>
          </ul>

        </ul>

      <button
        class="logout-btn"
        @click="logout"
      >
        Cerrar sesión
      </button>

    </aside>

    <main class="content">

<h1 class="title">
  Bienvenido {{ userName }}
</h1>

<p class="welcome">
  {{ role === 'admin'
      ? 'Panel de Administración'
      : 'Panel de Cliente' }}
</p>

      <div class="cards">

        <div class="card">
          <h3>Vehículos</h3>
          <p>0</p>
        </div>

        <div class="card">
          <h3>Citas</h3>
          <p>0</p>
        </div>

        <div class="card">
          <h3>Cotizaciones</h3>
          <p>0</p>
        </div>

        <div class="card">
          <h3>Órdenes</h3>
          <p>0</p>
        </div>

      </div>

    </main>

  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const userName = localStorage.getItem('userName')
const role = localStorage.getItem('role')

const vehiculosOpen = ref(false)
const citasOpen = ref(false)
const cotizacionesOpen = ref(false)
const ordenesOpen = ref(false)

const logout = () => {
  localStorage.removeItem('token')
  localStorage.removeItem('role')
  router.push('/login')
}
</script>

<style scoped>
.title{
  color:#b6ccff;
  font-size:28px;
  font-weight:700;
}

.welcome{
  color:#64748B;
  margin-bottom:30px;
}

.topbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;

  height: 70px;

  background: #0F172A;

  border-bottom: 3px solid #8B1E1E;

  display: flex;
  align-items: center;
  justify-content: space-between;

  padding: 0 25px;

  z-index: 1000;
}
.topbar-logo{
  height: 100px;
  width: auto;
  object-fit: contain;
}
.topbar-right{
  display:flex;
  align-items:center;
  gap:20px;
}

.user-panel{
  margin:0;
  text-align:right;
}
.menu-btn {
  background: transparent;
  border: none;
  color: white;
  font-size: 32px;
  cursor: pointer;
}

.topbar h2 {
  margin-left: auto;
  font-weight: 700;
}
.dashboard{
  display:flex;
  min-height:100vh;

  background-image:
    linear-gradient(
      rgba(15,23,42,.65),
      rgba(15,23,42,.65)
    ),
    url('/tokyo-bg.png');

  background-size:cover;
  background-position:center;
}

.sidebar{
  width:280px;

  background:
    rgba(2,6,23,.95);

  backdrop-filter:blur(8px);

  border-right:
    1px solid rgba(139,30,30,.4);

  display:flex;
  flex-direction:column;
  justify-content:space-between;

  padding:25px;
}
.sidebar-header{
  margin-bottom: 30px;
}
.sidebar.closed {
  margin-left: -330px;
  transform: translateX(-100%);
}

.sidebar h2 {
  margin-bottom: 30px;
  text-align: center;
}
.sidebar-logo{
  width: 220px;

  display: block;

  margin: 0 auto 25px auto;

  object-fit: contain;
}

.sidebar-user{
  text-align:center;
  margin-bottom:25px;
  padding-bottom:20px;
  border-bottom:1px solid rgba(255,255,255,.15);
}

.sidebar-user h4{
  margin:0;
  color:white;
}

.sidebar-user span{
  color:#CBD5E1;
  font-size:14px;
}
.user-panel{
  text-align:center;
  margin-bottom:25px;
}

.user-panel h4{
  margin-bottom:5px;
}

.user-panel span{
  color:#CBD5E1;
  font-size:14px;
}

.menu {
  list-style: none;
  padding: 0;
}
.menu-item {
  padding: 14px 18px;

  margin-bottom: 10px;

  border-radius: 12px;

  color: #CBD5E1;

  cursor: pointer;

  transition: all .3s ease;
}

.menu-item:hover {

  background:
    rgba(139,30,30,.25);

  color: white;

  transform:
    translateX(6px);

  box-shadow:
    0 0 10px rgba(139,30,30,.20);
}
.submenu li {

  padding: 10px;

  color: #94A3B8;

  cursor: pointer;

  transition: .3s;
}

.submenu li:hover {

  color: white;

  padding-left: 15px;
}


.logout-btn {
  width: 100%;
  padding: 12px;
  border: none;
  border-radius: 8px;
  background: white;
  color: #6e0f12;
  font-weight: bold;
  cursor: pointer;
}

.content {
  flex: 1;
  padding: 50px;
  transition: all .3s ease;
}

.cards {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}
.card {
  background: rgba(15,23,42,.55);

  backdrop-filter: blur(12px);

  border: 1px solid transparent;

  border-radius: 20px;

  padding: 30px;

  box-shadow:
    0 8px 20px rgba(0,0,0,.25);

  transition: all .3s ease;
}

.card:hover {

  transform: translateY(-6px);

  border-color: rgba(255, 0, 0, 0.61);

  box-shadow:
    0 0 5px rgba(139,30,30,.7),
    0 0 10px rgba(139,30,30,.6),
    0 0 20px rgba(139,30,30,.5),
    0 0 35px rgba(139,30,30,.3);
}
.card h3 {

  color:#E2E8F0;

  font-family:'Poppins',sans-serif;

  font-weight:500;
}
.card p {

  color:white;

  font-family:'Poppins',sans-serif;

  font-size:40px;

  font-weight:700;
}

</style>
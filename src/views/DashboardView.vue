<template>
    <div class="dashboard">

<aside
  class="sidebar">

    <div class="sidebar-header">
  <img
    src="/logo.png"
    class="sidebar-logo"
  />

</div>

        <ul class="menu">
           <li class="menu-item">
            <Home :size="18" />
  Inicio
</li>

<li
  class="menu-item"
  v-if="role === 'admin'"
>
<Users :size="18" />  
Usuarios
</li>

<li
  class="menu-item"
  v-if="role === 'client'"
>
  <User :size="18" />
  Mi Perfil
</li>

          <li
            class="menu-item"
            @click="vehiculosOpen = !vehiculosOpen"
          >
            {{ vehiculosOpen ? '▼' : '▶' }}
            <Car :size="18" />
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
            <Calendar :size="18" />
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
            <FileText :size="18" />
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
            <Wrench :size="18" />
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
<div class="content-topbar">

  <div class="page-title">
    Inicio
  </div>

  <div class="top-actions">

    <div class="notification">
       <Bell :size="20" />
      <span class="badge">3</span>
    </div>

    <div class="mini-user">
      {{ userName }}
    </div>

  </div>

</div>
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
    <div class="card-header">
      <Car :size="28" />
      <h3>Vehículos</h3>
    </div>

    <p>0</p>
  </div>

  <div class="card">
    <div class="card-header">
      <Calendar :size="28" />
      <h3>Citas</h3>
    </div>

    <p>0</p>
  </div>

  <div class="card">
    <div class="card-header">
      <FileText :size="28" />
      <h3>Cotizaciones</h3>
    </div>

    <p>0</p>
  </div>

  <div class="card">
    <div class="card-header">
      <Wrench :size="28" />
      <h3>Órdenes</h3>
    </div>

    <p>0</p>
  </div>

</main>

</div>

</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import {
  Bell,
  Home,
  Car,
  Calendar,
  FileText,
  Wrench,
  Users,
  User
} from 'lucide-vue-next'

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
.content-topbar{

  display:flex;

  justify-content:space-between;

  align-items:center;

  margin-bottom:40px;
}

.page-title{

  color:white;

  font-size:26px;

  font-weight:600;
}

.top-actions{

  display:flex;

  align-items:center;

  gap:30px;
}

.notification{

  position:relative;

  color:white;

  font-size:22px;

  cursor:pointer;
}

.badge{

  position:absolute;

  top:-8px;

  right:-10px;

  background:#8B1E1E;

  color:white;

  width:18px;

  height:18px;

  border-radius:50%;

  font-size:11px;

  display:flex;

  align-items:center;

  justify-content:center;
}

.mini-user{

  color:#CBD5E1;

  font-size:14px;
}
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
  width:250px;

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

   display:flex;
  align-items:center;
  gap:12px;
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

  padding: 25px;

  min-height: 180px;
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

  font-size:48px;

  font-weight:700;
  
  margin-top: 10px;
}
.card-header{

  display:flex;

  align-items:center;

  gap:12px;

  margin-bottom:20px;

  color:#CBD5E1;
}

</style>
<template>
  <div class="dashboard">

   <div class="topbar">
  <button
    class="menu-btn"
    @click="menuOpen = !menuOpen"
  >
    ☰
  </button>

  <h2>TallerSync</h2>  
</div>

<aside
  class="sidebar"
  :class="{ closed: !menuOpen }"
>
      <div>
        <h2>TallerSync</h2>

        <ul class="menu">

          <li class="menu-item">
            Inicio
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
      </div>

      <button
        class="logout-btn"
        @click="logout"
      >
        Cerrar sesión
      </button>

    </aside>

    <main class="content">

      <h1>Bienvenida a TallerSync</h1>

      <p class="welcome">
        Sistema de Gestión de Talleres Mecánicos
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

const vehiculosOpen = ref(false)
const citasOpen = ref(false)
const cotizacionesOpen = ref(false)
const ordenesOpen = ref(false)
const menuOpen = ref(true)

const logout = () => {
  localStorage.removeItem('token')
  router.push('/login')
}
</script>

<style scoped>
.topbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;

  height: 65px;

  background: #6e0f12;
  color: white;

  display: flex;
  align-items: center;

  padding: 0 20px;

  z-index: 1000;
}

.topbar h2 {
  margin-left: 15px;
}

.menu-btn {
  background: transparent;
  border: none;
  color: white;

  font-size: 26px;
  cursor: pointer;
}
.dashboard {
  display: flex;
  min-height: 100vh;
  background: #f8fafc;
  padding-top: 65px;
}

.sidebar {
  width: 280px;
  background: #6e0f12;
  color: white;

  display: flex;
  flex-direction: column;
  justify-content: space-between;

  padding: 25px;

  transition: all .3s ease;
}

.sidebar.closed {
  margin-left: -330px;
}

.sidebar h2 {
  margin-bottom: 30px;
  text-align: center;
}

.menu {
  list-style: none;
  padding: 0;
}

.menu-item {
  padding: 12px;
  margin-bottom: 8px;
  border-radius: 8px;
  cursor: pointer;
  transition: .2s;
}

.menu-item:hover {
  background: rgba(255,255,255,.15);
}

.submenu {
  list-style: none;
  margin-left: 20px;
  margin-bottom: 15px;
  padding-left: 10px;
}

.submenu li {
  padding: 8px;
  color: #f3f4f6;
  cursor: pointer;
}

.submenu li:hover {
  color: white;
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
  padding: 40px;
  transition: all .3s ease;
}

.welcome {
  color: gray;
  margin-bottom: 30px;
}

.cards {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}

.card {
  background: white;
  border-radius: 15px;
  padding: 25px;
  box-shadow: 0 10px 20px rgba(0,0,0,.08);
  transition: .2s;
}

.card:hover {
  transform: translateY(-3px);
}

.card h3 {
  margin-bottom: 10px;
}

.card p {
  font-size: 28px;
  font-weight: bold;
  color: #6e0f12;
}

</style>
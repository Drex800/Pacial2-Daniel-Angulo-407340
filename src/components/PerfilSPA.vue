<template>
  <div class="wrap">
    <header class="header" role="banner">
      <div class="brand">
        <div class="logo" aria-hidden="true">FB</div>
        <div>
          <h1>MiRed</h1>
          <p>Simulación de perfil - SPA</p>
        </div>
      </div>

      <div class="search" role="search">
        <label for="q" class="sr-only" style="position:absolute; left:-9999px">Buscar</label>
        <input
          id="q"
          placeholder="Buscar en MiRed... (ej: amigos, fotos, publicaciones)"
          autocomplete="off"
          v-model="busqueda"
        />
      </div>

      <div class="header-actions" aria-hidden="false">
        <button title="Notificaciones">🔔</button>
        <button title="Mensajes">✉️</button>
        <button title="Configuración">⚙️</button>
      </div>
    </header>

    <div class="main-grid">
      <aside class="profile" aria-label="Perfil de usuario">
        <div class="avatar">
          <img
            :src="usuario.avatar"
            alt="Avatar de usuario"
          />
          <div>
            <div class="username">{{ usuario.nombre }}</div>
            <div class="user-bio">{{ usuario.bio }}</div>
          </div>
        </div>

        <div class="profile-stats" role="list">
          <div class="stat" role="listitem">
            <strong>{{ usuario.amigos }}</strong>
            <div style="font-size:0.8rem">Amigos</div>
          </div>
          <div class="stat" role="listitem">
            <strong>{{ usuario.fotos }}</strong>
            <div style="font-size:0.8rem">Fotos</div>
          </div>
          <div class="stat" role="listitem">
            <strong>{{ usuario.boxes }}</strong>
            <div style="font-size:0.8rem">Boxes</div>
          </div>
        </div>

        <div style="margin-top:14px">
          <button
            id="editProfile"
            style="width:100%; padding:10px; border-radius:10px; border:0; background:var(--accent); color:white"
            @click="editarPerfil"
          >
            Editar perfil
          </button>
        </div>
      </aside>

      <main class="content" role="main">
        <div class="card">
          <nav class="profile-nav" role="navigation" aria-label="Navegación del perfil">
            <button
              v-for="seccion in secciones"
              :key="seccion"
              :class="{ active: vistaActual === seccion }"
              @click="cambiarVista(seccion)"
            >
              {{ seccion }}
            </button>
          </nav>

          <section id="view" aria-live="polite">
            <div v-if="vistaActual === 'Muro'">
              <p>Aquí aparecerían tus publicaciones recientes 📝</p>
            </div>
            <div v-else-if="vistaActual === 'Info'">
              <p>Información del perfil del usuario 📄</p>
            </div>
            <div v-else-if="vistaActual === 'Photos'">
              <p>Galería de fotos 📸</p>
            </div>
            <div v-else-if="vistaActual === 'Boxes'">
              <p>Tus boxes o colecciones 💼</p>
            </div>
          </section>
        </div>

        <footer>
          Hecho con Vue.js — Parcial. Usa Flexbox y Grid. HTML semántico.
        </footer>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "PerfilSPA",
  data() {
    return {
      busqueda: "",
      vistaActual: "Muro",
      secciones: ["Muro", "Info", "Photos", "Boxes"],
      usuario: {
        nombre: "Daniel Angulo",
        bio: "Estudiante · Apasionado por la física y el desarrollo web",
        avatar: "https://m.media-amazon.com/images/M/MV5BMjE2OTUwNTk4NF5BMl5BanBnXkFtZTcwMjMwOTk0NA@@._V1_.jpg",
        amigos: 324,
        fotos: 89,
        boxes: 56,
      },
    };
  },
  methods: {
    cambiarVista(vista) {
      this.vistaActual = vista;
    },
    editarPerfil() {
      alert("Funcionalidad de edición de perfil próximamente ✏️");
    },
  },
};
</script>

<style scoped>
/* Puedes adaptar tu style.css aquí o importarlo externamente */
.wrap {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background: #0077ff;
  color: white;
}

.brand {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.logo {
  background: white;
  color: #0077ff;
  border-radius: 50%;
  width: 35px;
  height: 35px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
}

.main-grid {
  display: grid;
  grid-template-columns: 250px 1fr;
  flex: 1;
}

.profile {
  background: #f4f4f4;
  padding: 1rem;
}

.avatar {
  display: flex;
  gap: 10px;
  align-items: center;
}

.avatar img {
  width: 70px;
  height: 70px;
  border-radius: 50%;
}

.profile-stats {
  display: flex;
  justify-content: space-around;
  margin-top: 10px;
}

.profile-nav button {
  margin: 5px;
  padding: 8px 14px;
  border: none;
  background: #eee;
  border-radius: 5px;
  cursor: pointer;
}

.profile-nav button.active {
  background: #0077ff;
  color: white;
}

footer {
  text-align: center;
  padding: 1rem;
  font-size: 0.9rem;
  color: gray;
}
</style>

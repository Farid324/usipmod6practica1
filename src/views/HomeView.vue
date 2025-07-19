<template>
  <div class="home">
    <h1>Agenda de Contactos</h1>

    <!-- Formulario -->
    <ContactFormComponent
      :editando="contactoEditando"
      @refrescar="obtenerContactos"
      @cancelar="contactoEditando = null"
    />

    <!-- Lista -->
    <ContactListComponent
      :contactos="listaContactos"
      @refrescar="obtenerContactos"
      @editar="contactoEditando = $event"
    />
  </div>
</template>

<script>
import ContactFormComponent from '../components/ContactFormComponent.vue'
import ContactListComponent from '../components/ContactListComponent.vue'
import axios from 'axios'

export default {
  components: {
    ContactFormComponent,
    ContactListComponent
  },
  data() {
    return {
      listaContactos: [],
      contactoEditando: null
    }
  },
  created() {
    this.obtenerContactos()
  },
  methods: {
    async obtenerContactos() {
      try {
        const res = await axios.get('http://localhost:3000/contactos')
        this.listaContactos = res.data
      } catch (error) {
        console.error('Error al obtener contactos:', error)
      }
    }
  }
}
</script>

<style scoped>
.home {
  max-width: 800px;
  margin: auto;
  padding: 2rem;
}
h1 {
  text-align: center;
  color: #2c3e50;
}
</style>
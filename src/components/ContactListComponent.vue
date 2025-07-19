<template>
  <div class="list-container">
    <h2>Lista de Contactos</h2>

    <input v-model="busqueda" placeholder="Buscar por nombre o email" />

    <ul>
      <li v-for="contacto in contactosFiltrados" :key="contacto.id">
        <strong>{{ contacto.name }}</strong> - {{ contacto.email }}<br />
        {{ contacto.address }} - {{ contacto.city }} ({{ contacto.country }})<br />
        📞 {{ contacto.phone }} <br />

        <button @click="$emit('editar', contacto)">Editar</button>
        <button @click="eliminarContacto(contacto.id)">Eliminar</button>
        <hr />
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: ['contactos'],
  emits: ['refrescar', 'editar'],
  data() {
    return {
      busqueda: ''
    }
  },
  computed: {
    contactosFiltrados() {
      return this.contactos.filter(c => {
        const criterio = this.busqueda.toLowerCase()
        return (
          c.name.toLowerCase().includes(criterio) ||
          c.email.toLowerCase().includes(criterio)
        )
      })
    }
  },
  methods: {
    async eliminarContacto(id) {
      if (confirm('¿Deseas eliminar este contacto?')) {
        try {
          await axios.delete(`http://localhost:3000/contactos/${id}`)
          this.$emit('refrescar')
        } catch (error) {
          console.error('Error al eliminar:', error)
        }
      }
    }
  }
}
</script>

<style scoped>
.list-container {
  background: #ffffff;
  padding: 1rem;
  border-radius: 8px;
  margin-top: 1rem;
}
input {
  width: 96%;
  margin-bottom: 12px;
  padding: 8px;
}
li {
  margin-bottom: 16px;
}
button {
  margin-right: 8px;
}
</style>

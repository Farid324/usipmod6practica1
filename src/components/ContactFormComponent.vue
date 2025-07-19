<template>
  <div class="form-container">
    <h2>{{ contacto.id ? 'Editar contacto' : 'Agregar contacto' }}</h2>
    <form @submit.prevent="guardarContacto" class="columnas">
      <input v-model="contacto.name" type="text" placeholder="Nombre" required />
      <input v-model="contacto.email" type="email" placeholder="Correo electrónico" required />
      <input v-model="contacto.address" type="text" placeholder="Dirección" />
      <input v-model="contacto.phone" type="text" placeholder="Teléfono" />
      <input v-model="contacto.country" type="text" placeholder="País" />
      <input v-model="contacto.city" type="text" placeholder="Ciudad" />
      <button type="submit">{{ contacto.id ? 'Actualizar' : 'Agregar' }}</button>
      <button v-if="contacto.id" type="button" @click="cancelarEdicion">Cancelar</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: ['editando'],
  emits: ['refrescar', 'cancelar'],
  data() {
    return {
      contacto: this.contactoVacio()
    }
  },
  watch: {
    editando(nuevo) {
      this.contacto = { ...nuevo }
    }
  },
  methods: {
    contactoVacio() {
      return {
        name: '',
        email: '',
        address: '',
        phone: '',
        country: '',
        city: ''
      }
    },
    async guardarContacto() {
      try {
        if (this.contacto.id) {
          await axios.put(`http://localhost:3000/contactos/${this.contacto.id}`, this.contacto)
        } else {
          await axios.post('http://localhost:3000/contactos', this.contacto)
        }
        this.$emit('refrescar')
        this.contacto = this.contactoVacio()
        this.$emit('cancelar')
      } catch (error) {
        console.error('Error al guardar:', error)
      }
    },
    cancelarEdicion() {
      this.contacto = this.contactoVacio()
      this.$emit('cancelar')
    }
  }
}
</script>

<style scoped>
.form-container {
  background: #f8f8f8;
  padding: 1rem;
  border-radius: 8px;
}
.columnas {
    display: flex;
}
input {
  display: block;
  width: 100%;
  margin-bottom: 10px;
  margin: 0px 5px;
  padding: 8px;
}
button {
  margin-right: 8px;
  padding: 8px 16px;
}
</style>
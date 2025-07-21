<template>
    <div class="container mt-4">
      <h4>Editar Contacto</h4>
  
      <form @submit.prevent="emitirDatosEditados" novalidate>
        <div class="mb-3">
          <label class="form-label">Nombre</label>
          <input v-model="editado.name" type="text" class="form-control" required />
        </div>
  
        <div class="mb-3">
          <label class="form-label">Correo Electronico</label>
          <input v-model="editado.email" type="text" class="form-control" required />
        </div>
  
        <div class="mb-3">
          <label class="form-label">Direccion</label>
          <input v-model="editado.address" type="text" class="form-control" required />
        </div>
  
        <div class="mb-3">
          <label class="form-label">Telefono</label>          
          <input v-model="editado.phone" type="text" class="form-control" required />
        </div>
  
        <div class="mb-3">
          <label class="form-label">Pais</label>          
          <input v-model="editado.country" type="text" class="form-control" required />
        </div>
  
        <div class="mb-3">
          <label class="form-label">Ciudad</label>
          <input v-model="editado.city" type="text" class="form-control" required />
        </div>
  
  
        <button type="submit" class="btn btn-success">Guardar Cambios</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ContactoEditar',
    props: {
      contacto: {
        type: Object,
        required: true
      }
    },
    data() {
      return {        
        editado: { ...this.contacto }
      }
    },
    methods: {
      emitirDatosEditados() {        
        this.$emit('update', this.editado)
      }
    }
  }
  </script>
  
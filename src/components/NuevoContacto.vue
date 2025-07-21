<template>
    <h1>{{ title }}</h1>

    <div class="container mt-4">
    <h2 class="mb-4">Registrar nuevo Contacto</h2>

    <form @submit.prevent="submit" novalidate>
      <div class="mb-3">
        <label class="form-label">Nombre</label>
        <input v-model="contacto.name" type="text" class="form-control" :class="{'is-invalid': v$.contacto.name.$error}" />
        <div class="invalid-feedback">name es obligatoria</div>
      </div>

      <div class="mb-3">
        <label class="form-label">Correo Electronico</label>
        <input v-model="contacto.email" type="text" class="form-control" :class="{'is-invalid': v$.contacto.email.$error}" />
        <div class="invalid-feedback">Correo es obligatorio</div>
      </div>

      <div class="mb-3">
        <label class="form-label">Direccion</label>
        <input v-model="contacto.address" type="text" class="form-control" :class="{'is-invalid': v$.contacto.address.$error}" />
        <div class="invalid-feedback">Direccion es obligatorio</div>
      </div>

      <div class="mb-3">
        <label class="form-label">Telefono</label>
        <input v-model="contacto.phone" type="text" class="form-control" :class="{'is-invalid': v$.contacto.phone.$error}" />
        <div class="invalid-feedback">Telefono es obligatorio</div>
      </div>

      <div class="mb-3">
        <label class="form-label">Pais</label>        
        <input v-model="contacto.country" type="text" class="form-control" :class="{'is-invalid': v$.contacto.country.$error}" />
        <div class="invalid-feedback">Pais es obligatorio</div>
      </div>

      <div class="mb-3">
        <label class="form-label">Ciudad</label>
        <input v-model="contacto.city" type="text" class="form-control" :class="{'is-invalid': v$.contacto.city.$error}" />
        <div class="invalid-feedback">Ciudad es obligatorio</div>
      </div>

      <button type="submit" class="btn btn-primary">Guardar</button>
    </form>
  </div>
  
</template>

<script>
import { reactive } from 'vue'
import useVuelidate from '@vuelidate/core'
import { required, minValue, maxValue, url } from '@vuelidate/validators'
export default {
    name: 'NuevoAutoView',
    data() {
        return {
            title: ' Nuevo Contacto',
            contacto: reactive({
                name: '',
                email: '',
                address: '',
                phone: '',
                country: '',
                city: ''
            }),
            v$: null
        }
    },
    components: {
        // Registro de componentes que se utilizaran.
    },
    created() {
        const currentYear = new Date().getFullYear()
        const rules = {
            contacto: {
                name: { required },
                email: { required },
                address: { required },
                phone: { required},
                country: { required},
                city: { required }
            }
        }
        this.v$ = useVuelidate(rules, { contacto: this.contacto })
    },
    methods: {
        // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
        async submit() {
            const isValid = await this.v$.$validate()
            if (!isValid) {
                alert('Por favor complete correctamente el formulario.')
                return
            }
            this.$emit('created', { ...this.contacto });
        }
    },
    computed: {
        // propiedades computadas que dependen de otras propiedades reactivas
    },
    props: {
        // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
}
</script>

<style></style>
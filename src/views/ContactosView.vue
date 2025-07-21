<template>
    <div class="container">
        <h1>{{ title }}</h1>
        <p><button type="button" class="btn btn-primary" @click="goToNew()">Nuevo</button></p>
        <div class="mb-3">
            <div class="input-group">
                <span class="input-group-text" id="basic-addon3">Filtrar por Nombre</span>
                <select v-model="marcaSeleccionado" id="address" class="form-select">
                    <option disabled value="">-- Selecciona --</option>
                    <option value="">Todos</option>
                    <option v-for="name in marcas" :key="name" :value="name">
                        {{ name }}
                    </option>
                </select>
            </div>
        </div>
        <div class="mb-3">
            <div class="input-group">
                <span class="input-group-text" id="basic-addon3" >Buscar por Nombre o Correo</span>
                <input type="search" v-model="nombreAbuscar"  class="form-control">
            </div>
        </div>
        <div>
            <table class="table table-bordered border-primary">
                <thead>
                    <tr>
                        <th scope="col">id</th>
                        <th scope="col">Nombre</th>
                        <th scope="col">Correo Electronico</th>
                        <th scope="col">Direccion</th>
                        <th scope="col">Telefono</th>
                        <th scope="col">Pais</th>
                        <th scope="col">Ciudad</th>
                        <th></th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(item, index) in getItems" :key="item.id">
                        <th scope="row">{{ item.id }}</th>
                        <td>{{ item.name }}</td>
                        <td>{{ item.email }}</td>
                        <td>{{ item.address }}</td>
                        <td>{{ item.phone }}</td>
                        <td>{{ item.country }}</td>
                        <td>{{ item.city }}</td>
                        <td><button type="button" class="btn btn-primary" @click="abrirModal(index)">
                                Editar
                            </button>
                            <button type="button" class="btn btn-danger" @click="eliminar(index)">
                                eliminar
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>

    </div>


    <!-- Modal Bootstrap -->
    <div class="modal fade" id="modalAutoEditar" tabindex="-1" aria-labelledby="modalAutoEditarLabel" aria-hidden="true"
        ref="modalRef">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="modalAutoEditarLabel">Editar Contacto</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Cerrar"></button>
                </div>
                <div class="modal-body">
                    <!-- Componente ContactoEditar -->
                    <ContactoEditar v-if="modalMode =='editar' && contactoSeleccionado" :contacto="contactoSeleccionado" @update="guardarEdicion"
                        @cancelar="cerrarModal" />
                    <NuevoContacto v-if="modalMode =='crear'" @created="agregarNuevo($event)"></NuevoContacto>    
                </div>
            </div>
        </div>
    </div>

</template>

<script>
import ContactoEditar from '../components/ContactoEditar.vue';
import NuevoContacto from '../components/NuevoContacto.vue';
export default {
    name: 'Contactos',
    data() {
        return {
            title: 'Contactos',
            items: [
                {
                    id: 1,
                    name: "Alice Johnson",
                    email: "alice.johnson@example.com", // modelo
                    address: "123 Maple Street",
                    phone: "123-456-7890",
                    country: "USA",
                    city: "New York"
                },
                {
                    id: 2,
                    name: "Bob Smith",
                    email: "bob.smith@example.com",
                    address: "456 Oak Avenue",
                    phone: "987-654-3210",
                    country: "Canada",
                    city: "Toronto"
                },
                {
                    id: 3,
                    name: "Carol White",
                    email: "carol.white@example.com",
                    address: "789 Pine Road",
                    phone: "555-123-4567",
                    country: "UK",
                    city: "London"
                },
                {
                    id: 4,
                    name: "David Brown",
                    email: "david.brown@example.com",
                    address: "321 Elm Street",
                    phone: "444-555-6666",
                    country: "Australia",
                    city: "Sydney"
                },
                {
                    id: 5,
                    name: "Emily Davis",
                    email: "emily.davis@example.com",
                    address: "654 Spruce Lane",
                    phone: "333-444-5555",
                    country: "USA",
                    city: "Los Angeles"
                }
            ],
            modalBootstrapInstance: null,
            contactoSeleccionado: null,
            indiceSeleccionado: 0,
            marcas: [
                'Toyota',
                'Honda',
                'Ford',
                'Chevrolet',
                'Nissan',
                'Hyundai',
                'Kia',
            ],
            marcaSeleccionado: "",
            nombreAbuscar:"",
            modalMode:"crear"
        }
    },
    components: {
        // Registro de componentes que se utilizaran.
        ContactoEditar,
        NuevoContacto,
    },
    mounted() {
        this.$nextTick(() => {
            if (this.$refs.modalRef) {
                this.modalBootstrapInstance = new bootstrap.Modal(this.$refs.modalRef);
            } else {
                console.error('No se encontró el ref modalRef');
            }
        });
    },
    methods: {
        // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
        goToNew() {
            this.modalMode="crear";
            if (this.modalBootstrapInstance) {
                this.modalBootstrapInstance.show();
                
            } else {
                console.error('modalBootstrapInstance no está inicializado');
            }
        },
        abrirModal(index) {
            this.contactoSeleccionado = null;
            this.indiceSeleccionado = index;
            this.modalMode="editar";
            setTimeout(() => {
                if (this.modalBootstrapInstance) {
                    this.modalBootstrapInstance.show();
                    this.contactoSeleccionado = { ...this.items[index] };
                } else {
                    console.error('modalBootstrapInstance no está inicializado');
                }
            });

        },
        cerrarModal() {
            if (this.modalBootstrapInstance) {

                this.modalBootstrapInstance.hide();
            }
        },
        guardarEdicion(autoEditado) {
            console.log('Contacto editado:', autoEditado);
            // Aquí actualizas la info, haces llamada a API, etc.
            this.items[this.indiceSeleccionado] = autoEditado;
            this.cerrarModal();
        },

        eliminar(index) {
            if (confirm('¿Está seguro de eliminar este Contacto?')) {
                this.items.splice(index, 1);
            }
        },
        agregarNuevo($event){
            const maxId = Math.max(...this.items.map(contacto => contacto.id));
            $event['id'] = maxId + 1;
            this.items.push($event);
            console.log($event);
            this.cerrarModal();
        }

    },
    computed: {
        // propiedades computadas que dependen de otras propiedades reactivas
        getItems() {
            let result = [...this.items];
            if (this.marcaSeleccionado !== "") {
                result = this.items.filter((item) => { return item.name === this.marcaSeleccionado; });
            }

            if(this.anioAbuscar !== ""){
                result = result.filter((item) => { 
                    const _marca = item.modelo || "";
                    const _textToSearch = this.nombreAbuscar || "";
                    return _marca.toLowerCase().includes(_textToSearch.toLocaleLowerCase()); 
                });
            }

            return result;
        }
    },
    props: {
        // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
}
</script>

<style></style>
<template>
    <div>
        <RouterLink class="btn btn-primary m-2 float-end" to="/add-empleados">Registrar area</RouterLink>
        <table class="table table-striped">
            <thead>
                <tr>
                    <th>
                        Id
                    </th>
                    <th>
                        Nombre
                    </th>
                    <th>
                        Acción
                    </th>
                </tr>
            </thead>

            <tbody>
                <tr v-for="(are, index) in this.areas" :key="index">
                    <td>{{ are.id }}</td>
                    <td>{{ are.name }}</td>
                    <td>
                        <RouterLink class="btn btn-warning" :to="`/edit-areas/${are.id}`">Edit</RouterLink>
                        <button type="button" @click="openDeleteModal" class="btn btn-danger">delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'AreaView',
    data() {
        return {
            modalTitle: "",
            areas: [],
            id: 0,
            name: "",
            isLoading: false
        };
    },
    methods: {
        refreshData() {
            axios.get('http://localhost:3001/areas')
                .then((response) => {
                    this.areas = response.data;
                });
        },

        addClick() {
            this.modalTitle = "Registrar areas";
            this.id = 0;
            this.name = "";
        },
        editClick(are) {
            this.modalTitle = "Edit Area";
            this.id = are.id;
            this.name = are.name;
        },
        createClick() {
            axios.post("area", {
                PersonaNombre: this.PersonaNombre,
                PersonaPaterno: this.PersonaPaterno,
                PersonaMaterno: this.PersonaMaterno,
                PersonaTelefono: this.PersonaTelefono
            })
                .then((response) => {
                    this.refreshData();
                    alert(response.data);
                });
        },
        updateClick() {
            axios.put("area", {
                id: this.id,
                name: this.name,
            })
                .then((response) => {
                    this.refreshData();
                    alert(response.data);
                });
        },
        deleteClick(id) {
            if (!confirm("Está seguro de eliminar?")) {
                return;
            }
            axios.delete("area/" + id)
                .then((response) => {
                    this.refreshData();
                    alert(response.data);
                });
        }
    },
    mounted() {
        //      this.isLoading= true;
        this.refreshData();
    }
    //   components: { ConfirmDeleteModal }
};
</script>
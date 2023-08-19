<template>
    <div class="row">
        <div class="col -lg -10 offset-lg-0">
            <div class="table-responsive">
                <DataTable :data="empleados" :columns="columns" class="table table-striped table-bordered display"
                :options="{responsive: true, autoWidth: false, dom: 'Bfrtip', language: {
                    search: 'Buscar', zeroRecords: 'No hay registros para mostrar',
                    info: 'Mostrando del _START_ a _END_  de _TOTAL_ registros',
                    infoFiltered: '(Filtrados de  _MAX_ registros.)',
                    paginate: {
                        first: 'Primero', previous: 'Anterior', next: 'Siguiente', last: 'Último'
                    }
                }, buttons: botones}">
                    <thead>
                        <tr><th>no</th><th>Nombre</th><th>Area</th><th>tipo</th><th>color</th><th>placa</th></tr>
                    </thead>
                </DataTable>
            </div>
        </div>
    </div>
</template>
<script>
    import axios from 'axios';
    import DataTable from 'datatables.net-vue3';
    import DataTableLib from 'datatables.net-bs5'
    import ButtonsHtml5 from 'datatables.net-buttons/js/buttons.html5'
    import pdfmake from 'pdfmake';
    import pdfFonts from 'pdfmake/build/vfs_fonts';
    pdfmake.vfs = pdfFonts.pdfMake.vfs;
    import 'datatables.net-responsive-bs5';
    import JsZip from 'jszip';
    window.JSZip = JsZip;
    DataTable.use(DataTableLib);
    DataTable.use(pdfmake);
    DataTable.use(ButtonsHtml5);

    export default{
        components: {DataTable},
        data(){
            return {
                empleados: null,
                columns: [
                    {data: null, render: function(data, type, row, meta)
                        {return `${meta.row+1}`}},
                        {data: 'name'},
                        {data: 'areasId'},
                        {data: 'typesId'},
                        {data: 'color'},
                        {data: 'placa'}
                ],
                botones: [
                    {
                        title: 'Reporte de empleados',
                        extend: 'excelHtml5',
                        text: '<i class="bi bi-file-excel"></i> Excel',
                        className: 'btn btn-success'
                    },
                    {
                        title: 'Reporte de empleados',
                        extend: 'pdfHtml5',
                        text: '<i class="bi bi-file-pdf"></i> PDF',
                        className: 'btn btn-danger'
                    }
                ]
            }
        },
        mounted() {
            this.getEmpleados();
        }, 
        methods: {
            getEmpleados(){
                axios.get('http://localhost:3001/employees').then(
                    response => (
                        this.empleados = response.data
                    )
                );
            }
        }
    }
</script>
<style>
@import 'bootstrap';
@import 'datatables.net-bs5';
</style>
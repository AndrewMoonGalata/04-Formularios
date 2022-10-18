<script>
export default {
    props: ['numeroProyectos', 'proyectos', 'cambiarUrgencia', 'limpiarData', 'deleteItem'],
}
</script>

<template>
    <div class="row">
        <div class="col-6 text-start">
            <h3 class="my-4 ml-auto"> Total de proyectos: {{numeroProyectos}}</h3>
        </div>
        <div class="col-6 text-end">
            <button class="btn btn-danger my-4" @click="limpiarData">Limpiar proyectos</button>
        </div>
    </div>
    <div class="table-responsive">
        <table class="table table-dark ">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Proyecto</th>
                    <th>Tipo</th>
                    <th>Urgente</th>
                    <th>Completado</th>
                    <th>Acciones</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(proyect, index) in proyectos" class="align-items-center">
                    <td>{{index+1}}</td>
                    <td>{{proyect.proyecto}}</td>
                    <td>{{proyect.tipo}}</td>
                    <td @click="cambiarUrgencia(proyect, 'urgente')"
                        :class="proyect.urgente ? 'bg-success':'bg-danger'">{{proyect.urgente ? "Si":"No"}}</td>
                    <td @click="cambiarUrgencia(proyect, 'completado')"
                        :class="proyect.completado ?  'bg-success':'bg-warning text-dark' "> {{proyect.completado ?
                        "Completado" : "Incompleto" }}</td>
                    <td><button class="btn btn-danger" @click="deleteItem(index)"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16"
                                fill="currentColor" class="bi bi-trash3-fill" viewBox="0 0 16 16">
                                <path
                                    d="M11 1.5v1h3.5a.5.5 0 0 1 0 1h-.538l-.853 10.66A2 2 0 0 1 11.115 16h-6.23a2 2 0 0 1-1.994-1.84L2.038 3.5H1.5a.5.5 0 0 1 0-1H5v-1A1.5 1.5 0 0 1 6.5 0h3A1.5 1.5 0 0 1 11 1.5Zm-5 0v1h4v-1a.5.5 0 0 0-.5-.5h-3a.5.5 0 0 0-.5.5ZM4.5 5.029l.5 8.5a.5.5 0 1 0 .998-.06l-.5-8.5a.5.5 0 1 0-.998.06Zm6.53-.528a.5.5 0 0 0-.528.47l-.5 8.5a.5.5 0 0 0 .998.058l.5-8.5a.5.5 0 0 0-.47-.528ZM8 4.5a.5.5 0 0 0-.5.5v8.5a.5.5 0 0 0 1 0V5a.5.5 0 0 0-.5-.5Z" />
                            </svg> Eliminar
                        </button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<style scoped>
td.bg-success,
td.bg-danger,
td.bg-warning {
    cursor: pointer;
}
</style>
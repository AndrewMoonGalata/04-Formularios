<script>
import ProgressBar from './ProgressBar.vue';
import TotalProyectos from './TotalProyectos.vue';
export default {
    data: () => ({
        proyecto: "",
        tipo: "",
        urgente: false,
        proyectos: [],
    }),
    methods: {
        cambiarUrgencia(proyecto, campo) {
            console.log(proyecto, campo);
            proyecto[campo] = !proyecto[campo];
            this.saveData();
        },
        regsitrarProyecto() {
            const proyecto = {
                proyecto: this.proyecto,
                tipo: this.tipo,
                urgente: this.urgente,
                completado: false,
            };
            this.proyectos.push(proyecto);
            this.saveData();
            console.warn("Proyecto regsitrado\n", this.proyectos);
            this.proyecto = "";
            this.tipo = "";
            this.urgente = false;
        },
        deleteItem(index){
            this.proyectos[index]="";
            this.proyectos.splice(index, 1);
            localStorage.clear(this.proyectos.index);
            this.saveData();
        },
        saveData(){
            localStorage.setItem("proyectos", JSON.stringify(this.proyectos));
        },
        limpiarData(){
            localStorage.clear();
            this.proyectos = [];
        },
    },
    computed: {
        numeroProyectos() {
            return this.proyectos.length;
        },
        porcentaje() {
            var completados = 0;
            this.proyectos.map(proyecto => {
                if (proyecto.completado)
                    completados++;
            });
            return isNaN((completados * 100) / this.numeroProyectos) ? 0 : parseInt((completados * 100) / this.numeroProyectos);
        }
    },
    components: { ProgressBar, TotalProyectos },
    mounted() {
        this.proyectos = JSON.parse(localStorage.getItem("proyectos")) || [];
    }
};
</script>

<template>
    <div class="row">
        <div class="col-12">
            <progress-bar :porcentaje="porcentaje"/>
        </div>
        <div class="col-12 col-md-4">
            <form @submit.prevent="regsitrarProyecto" class="mt-4">
                <div class="mb-3">
                    <label class="form-label"> Proyecto </label>
                    <input class="form-control" type="text" v-model.trim="proyecto" placeholder="Nombre de Proyecto"
                        required />
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">Actividades</label>
                    <select name="" id="" class="form-select" v-model="tipo" required>
                        <option selected disabled value="">Seleciona un tipo de actividad</option>
                        <option>Aplicaciones Web con Vue.js</option>
                        <option>Backend Services con Node.js</option>
                        <option>App movil con React Native</option>
                    </select>
                </div>
                <div class="mb-3">
                    <label class="form-check-label">Urgente </label>
                    <input v-model="urgente" class="form-check-input" type="checkbox" />
                </div>
                <button class="btn btn-success btn-block" type="submit">Enviar</button>
            </form>
        </div>
        
        <div class="col-12 col-md-8">
            <total-proyectos :numeroProyectos="numeroProyectos" :proyectos="proyectos" :cambiarUrgencia="cambiarUrgencia" :limpiarData="limpiarData" :deleteItem="deleteItem" />
        </div>
    </div>
</template>

<style scoped>
.form-check-label {
    margin-right: 0.5rem !important;
}

td.bg-success,
td.bg-danger {
    cursor: pointer;
}
</style>
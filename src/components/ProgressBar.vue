<script>
export default {
    props: {
        porcentaje: Number
    }
}
</script>

<template>
    <h3 class="text-center">
        Progreso {{porcentaje}}%
    </h3>
    <div class="progress my-4">
        <div class="progress-bar progress-bar-striped progress-bar-animated bg-success" role="progressbar"
            :style="{width: porcentaje+'%'}" v-bind:aria-valuenow="porcentaje" aria-valuemin="0" aria-valuemax="100">
        </div>
    </div>
</template>

<style>

</style>
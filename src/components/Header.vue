<script>
export default {
    data: () => ({
        url: "https://cdn.svgporn.com/logos/vue.svg",
        msg: "Vue.js",
    }),
};
</script>

<template>
    <div class="row">
        <div class="col">
            <h1>Formularios</h1>
            <img width="100" :src="url" :alt="msg" class="my-4">
        </div>
    </div>
    <hr />
</template>
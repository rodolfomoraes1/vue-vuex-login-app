<template>
    <div class="card text-center col-6 mx-auto mt-4">
        <div class="card-header">
            Vue + Vuex app
        </div>
        <div class="card-body">
            <h5 class="card-title">Frontend</h5>
            <p class="card-text">This app was built using Vue, Vuex, bootstrap 4</p>

            <h5 class="card-title">Backend</h5>
            <p class="card-text">The server side of this app was built using node, express, mongo, mongoose, Json Web Token</p>
        </div>
        <div class="card-footer text-muted">
            By Rodolfo Moraes Martins
        </div>
        <router-link to="/login" class="btn btn-link">Back</router-link>
    </div>
</template>

<script>
    export default {
    }
</script>

<style scoped>

</style>
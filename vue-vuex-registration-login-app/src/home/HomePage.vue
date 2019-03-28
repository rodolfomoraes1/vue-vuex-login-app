<template>
    <div class="col-8 mx-auto mt-5">
        <h1>Users List</h1>

        <h5 class="mt-2">Logged user: {{account.user.name}}</h5>

        <em v-if="users.loading">Loading users...</em>
        <span v-if="users.error" class="text-danger">ERROR: {{users.error}}</span>

        <ul class="list-group" v-if="users.items">
            <li class="list-group-item disabled" v-for="user in users.items" :key="user.id">
                {{user.name}} - {{user.email}}
            </li>
        </ul>

        <button class="btn btn-light m-1">
            <router-link to="/register">Register New User</router-link>
        </button>
        <button class="btn btn-light m-1">
            <router-link to="/login">Logout</router-link>
        </button>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    computed: {
        ...mapState({
            account: state => state.account,
            users: state => state.users.all
        })
    },
    created () {
        this.getAllUsers();
    },
    methods: {
        ...mapActions('users', {
            getAllUsers: 'getAll'
        })
    }
};
</script>
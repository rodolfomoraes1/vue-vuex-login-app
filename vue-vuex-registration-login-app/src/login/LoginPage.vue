<template>
    <div class="card col-6 mx-auto mt-4">
        <div class="card-header">
            <h3>Login</h3>
            <div class="card-body">
                <form class="form" @submit.prevent="handleSubmit">
                    <div class="form-group">
                        <label>Email</label>
                        <input type="email" v-model="email" name="email" class="form-control" :class="{ 'is-invalid': submitted && !email }" />
                        <div v-show="submitted && !email" class="invalid-feedback">Email is required</div>
                    </div>

                    <div class="form-group">
                        <label>Password</label>
                        <input type="password" v-model="password" name="password" class="form-control" :class="{ 'is-invalid': submitted && !password }" />
                        <div v-show="submitted && !password" class="invalid-feedback">Password is required</div>
                    </div>

                    <div class="form-group">
                        <button class="btn btn-primary" :disabled="status.loggingIn">Login</button>
                        <router-link to="/register" class="btn btn-link">Register</router-link>
                        <router-link to="/about" class="btn btn-link">About</router-link>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    data () {
        return {
            email: '',
            password: '',
            submitted: false
        }
    },
    computed: {
        ...mapState('account', ['status'])
    },
    created () {
        // reset login status
        this.logout();
    },
    methods: {
        ...mapActions('account', ['login', 'logout']),
        handleSubmit (e) {
            this.submitted = true;
            const { email, password } = this;
            if (email && password) {
                this.login({ email, password })
            }
        }
    }
};
</script>
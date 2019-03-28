<template>
    <div class="card col-6 mx-auto mt-4">
        <div class="card-header">
            <h3>Register</h3>
            <div class="card-body">
                <form class="form" @submit.prevent="handleSubmit">
                    <div class="form-group">
                        <label>Name</label>
                        <input type="name" v-model="user.name" v-validate="'required'" name="name" class="form-control" :class="{ 'is-invalid': submitted && errors.has('name') }" />
                        <div v-if="submitted && errors.has('name')" class="invalid-feedback">{{ errors.first('name') }}</div>
                    </div>
                    <div class="form-group">
                        <label>Email</label>
                        <input type="email" v-model="user.email" v-validate="'required'" name="email" class="form-control" :class="{ 'is-invalid': submitted && errors.has('email') }" />
                        <div v-if="submitted && errors.has('email')" class="invalid-feedback">{{ errors.first('email') }}</div>
                    </div>

                    <div class="form-group">
                        <label>Password</label>
                        <input type="password" v-model="user.password" v-validate="{ required: true, min: 8 }" name="password" class="form-control" :class="{ 'is-invalid': submitted && errors.has('password') }" />
                        <div v-if="submitted && errors.has('password')" class="invalid-feedback">{{ errors.first('password') }}</div>
                    </div>

                    <div class="form-group">
                        <button class="btn btn-primary" :disabled="status.registering">Register</button>
                        <router-link to="{ path: $store.state.route.from.fullPath }" class="btn btn-link">Cancel</router-link>
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
            user: {
                name: '',
                email: '',
                password: ''
            },
            submitted: false
        }
    },
    computed: {
        ...mapState('account', ['status'])
    },
    methods: {
        ...mapActions('account', ['register']),
        handleSubmit(e) {
            this.submitted = true;
            this.$validator.validate().then(valid => {
                if (valid) {
                    this.register(this.user);
                }
            });
        }
    }
};
</script>
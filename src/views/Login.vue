<template>
    <div class="container">
        <b-form @submit="onSubmit">
            <b-form-group id="input-group-1" label="Username:" label-for="input-1"
                description="We'll never share your username with anyone else.">
                <b-form-input id="input-1" v-model="form.username" type="text" placeholder="Enter username" required>
                </b-form-input>
            </b-form-group>

            <div class="row"></div>

            <b-form-group id="input-group-2" label="Password:" label-for="input-2">
                <b-form-input id="input-2" v-model="form.password" type="password" placeholder="Enter password"
                    required></b-form-input>
            </b-form-group>

            <b-button type="submit" variant="primary">Submit</b-button>
        </b-form>
        <b-card class="mt-3" header="Form Data Result">
            <pre class="m-0">{{ form }}</pre>
        </b-card>
    </div>
</template>

<script>
    import axios from "axios";

    export default {
        data() {
            return {
                form: {
                    username: '',
                    password: ''
                },
            }
        },
        methods: {
            onSubmit(event) {
                event.preventDefault()

                axios.post('https://dev-account-manager.herokuapp.com/login', {
                        username: this.form.username,
                        password: this.form.password
                    })
                    .then(function (response) {
                        console.log(response);
                        // this.$router.push('Home');
                        sessionStorage.setItem("token", "aasdf")
                        this.$router.push({
                            name: 'Home'
                        });
                    })
                    .catch(function (error) {
                        console.log(error);
                        // console.log(error.response.data);
                        // console.log(error.response.status);
                        // console.log(error.response.headers);
                    })
            },
        },
        mounted() {
            axios.get('https://dev-account-manager.herokuapp.com/ping')
                .then(function (response) {
                    console.log(response);
                })
                .catch(function (error) {
                    console.log(error.data);
                    alert('server is not ready');
                })
        },
    }
</script>
<template>
    <v-layout column justify-center align-center>
        <v-flex xs12 sm8 md6>
            <v-card min-width="350">
                <v-card-text>
                    <v-card-title class="title">
                        <h2>Log In</h2>
                    </v-card-title>
                    <v-form ref="form" v-model="valid" lazy-validation>
                        <v-text-field v-model="name" :counter="16" :rules="nameRules" label="Name" required></v-text-field>

                        <v-text-field v-model="password" :rules="passRules" type="password" label="Password" required></v-text-field>

                        <v-card-actions class="btn">
                            <v-btn :disabled="!valid" color="success" class="mr-4" @click="submit">
                                Sign in
                            </v-btn>

                            <v-btn color="error" class="mr-4" @click="reset">
                                Reset Form
                            </v-btn>
                        </v-card-actions>

                    </v-form>
                </v-card-text>
            </v-card>
        </v-flex>
    </v-layout>
</template>

<script>
    import {mapMutations} from 'vuex'
    export default {
        layout: 'logIn',
        data: () => ({
            valid: true,
            name: '',
            nameRules: [
                v => !!v || 'Name is required',
                v => (v && v.length <= 16) || 'Name must be less than 16 characters',
            ],
            password: '',
            passRules: [
                v => !!v || 'Password is required',
                v => /[a-zA-Z0-9]/.test(v) || 'Use english letters and numbers',
                v => (v && v.length >= 4) || 'Password must be at least 4 characters',
            ]
        }),

        methods: {
            ...mapMutations(["user"]),
            submit() {
                if(this.$refs.form.validate()){
                    const user = {
                       name: this.name,
                       password: this.password    
                    }
                    this.user(user);
                    this.$router.push("/profile"); 
                }
            },
            reset() {
                this.$refs.form.reset()
            }
        },
    }

</script>

<style scoped>
    .title {
        justify-content: center;
    }
    
    .btn {
        justify-content: center;
    }

</style>

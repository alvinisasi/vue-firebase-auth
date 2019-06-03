<template>
    <v-container>
        <v-form
            ref="form"
            v-model="valid"
            lazy-validation
        >
            <v-text-field
                v-model="email"
                :rules="emailRules"
                label="Email"
                required
            ></v-text-field>
            <v-text-field
                v-model="password"
                :rules="passwordRules"
                label="Password"
                :append-icon="passwordShow ? 'visibility' : 'visibility_off'"
                :type="passwordShow ? 'text' : 'password'"
                @click:append="passwordShow = !passwordShow"
                required
            ></v-text-field>

            <v-btn color="success" @click="validate">login</v-btn>
        </v-form>
    </v-container>
</template>

<script>
/* eslint-disable */
import * as firebase from 'firebase'
export default {
    data: () => ({
        valid: true,
        passwordShow: false,
        email: '',
        emailRules: [
            v => !!v || 'Email is required',
            v => /.+@.+/.test(v) || 'E-mail must be valid'
        ],
        password: '',
        passwordRules: [
            v => !!v || 'Passwod & Confirm Password are required'
        ]
    }),
    methods: {
       validate(){
            if (this.$refs.form.validate()){
                this.snackbar = true
            }
            this.loginWithFirebase()
        },
        loginWithFirebase() {
        firebase.auth().signInWithEmailAndPassword(this.email, this.password)
            .then((response) => {
            alert('success')
            console.log(response)
            })
            .catch((error) => {
            alert('failure')
            console.log(error)
            })
        }
    },
}
</script>
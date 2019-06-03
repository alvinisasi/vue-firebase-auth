<template>
  <v-container >
      <v-form
            ref="form"
            v-model="valid"
            lazy-validation
          >
            <v-text-field
                v-model="email"
                :rules="emailRules"
                label="E-mail"
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
            <v-text-field
                v-model="confirmPassword"
                :rules="passwordRules"
                label="Confirm Password"
                :append-icon="confirmPasswordShow ? 'visibility' : 'visibility_off'"
                :type="confirmPasswordShow ? 'text' : 'password'"
                @click:append="confirmPasswordShow = !confirmPasswordShow"
                required
            ></v-text-field>

            <v-btn color="success" @click="validate">register</v-btn>
            <v-btn color="error" @click="reset">reset</v-btn>
        </v-form>
  </v-container>
</template>

<script>
import * as firebase from 'firebase'
/* eslint-disable */
export default {
    data: () => ({
        passwordShow: false,
        confirmPasswordShow: false,
        valid: true,
        email: '',
        emailRules: [
            v => !!v || 'Email is required',
            v => /.+@.+/.test(v) || 'E-mail must be valid'
        ],
        password: '',
        passwordRules: [
            v => !!v || 'Passwod & Confirm Password are required'
        ],
        confirmPassword: ''
    }),
    methods: {
        validate(){
            if (this.$refs.form.validate()){
                this.snackbar = true
            }
            this.registerWithFirebase()
        },
        reset(){
            this.$refs.form.reset()
        },
        registerWithFirebase () {
        firebase.auth().createUserWithEmailAndPassword(this.email, this.password)
            .then((response) => {
            alert('success')
            console.log(response)
            })
            .catch((error) => {
            alert('failure')
            console.log(error)
            })
        }
    }
}
</script>
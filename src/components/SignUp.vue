<template>
    <div class="signUp">
        <div class="container-fluid">
            <div class="row">
                <div class="headerBackground">
                <h3 style="padding-top:  20px;"> {{ msg }}</h3>
                </div>
            </div>
        </div>
        <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <form @submit.prevent="signUp">
            <img src="../assets/image.png" alt="Chat Image" class="img-responsive">
            <br><br>
            <!-- Email Address -->
            <input type="text" placeholder="Enter Email Address" class="form-control" v-model="email">
            <br>
            <!-- Password -->
            <input type="password" placeholder="Ener Password" class="form-control" v-model="password">
            <br>
            <!-- Submit Button -->
            <button class="btn btn-primary"> Sign Up</button>
             <p class="signUpLink">
                You have an account? <router-link to="/login">Login here</router-link>
            </p>
            <!-- <hr> -->
        </form>
        </div>
    </div>
</template>

<script>
import firebase from 'firebase';
import nativeToast from 'native-toast';
    export default {
        data() {
            return {
                msg: 'A Vue Chat App With Firebase Realtime Database',
                email: '',
                password: ''
            }
        },
        methods: {
            signUp() {
                // this.$router.replace('ChatHome');
                // The createUserWithEmailAndPassword function return a Firebase promise, with an onResolve and onReject callback.
                // then(onResolve, onReject).  

                firebase.auth().createUserWithEmailAndPassword(this.email, this.password).then(user => {
                    nativeToast({
                        message: 'Account created Successfully!!!',
                        type: 'success',
                        icon: false
                    })   
                    this.email = '',
                    this.password = ''
                    this.$router.replace('ChatHome');
                }, err => {
                    alert('Oops... Something went wrong!!!' + err.message);
                });
            }
        }
    }
</script>


<style>
</style>


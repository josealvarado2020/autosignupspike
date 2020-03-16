<template>
  <div class="home">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <br>
    <input v-model="username" placeholder="username">
    <br>
    <input v-model="password" placeholder="password">
    <br>
    <br>
    <button type="button" class="btn btn-primary btn-lg" @click="login">Login test</button>
    <br>
    <br>
    <input v-model="signupemail" placeholder="sign up email">
    <br>
    <button type="button" class="btn btn-primary btn-lg" @click="signup">Sign up test</button>
    <br>
    <br>
    <br>
    <input v-model="code" placeholder="code">
    <br>
    <br>
    <button type="button" class="btn btn-primary btn-lg" @click="confirmsignup"> confirm Sign up test</button>
    <br>
    <br>
    <button type="button" class="btn btn-primary btn-lg" @click="resendsignup"> resend code</button>        

  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import { Auth } from 'aws-amplify';
export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data() {
    return {
      username: '',
      password: '',
      signupemail: '',
      code: ''
    }
  },
  methods: {
    async login() {
      await Auth.signIn(this.username, this.password);
      const user = await Auth.currentAuthenticatedUser();
      console.log(user);
    },
    async signup() {
      try {
          // const attributes = {
          //   email : "test2@me.com",
          //   phone_number: "0422222222",
          // };
        const data = await Auth.signUp(this.signupemail, "Password123!");
        console.log(data);
      } catch (err) {
        console.error(err);
      }
    },
    async confirmsignup() {
      try {
        const data = await Auth.confirmSignUp(this.signupemail, this.code);
        console.log(data);
      } catch (err) {
        console.error(err);
      }
    },
    async resendsignup() {
      try {
        const data = await Auth.resendSignUp(this.signupemail);
        console.log(data);
        console.log("code resent");
      } catch (err) {
        console.error(err);
      }
    }
  }
}
</script>

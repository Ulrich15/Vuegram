<template>
  <div id="login">
    <PasswordReset v-if="showPasswordReset" @close="togglePasswordReset" />
    <section>
      <div class="col1">
        <h1>Vuegram</h1>
        <p>
          Welcome to the
          <a href="https://savvyapps.com/" target="_blank">Ulrich Apps</a> Une application simple de connexion pour se familairiser avec
          le système de login de VueJs et  Firebase.
        </p>
      </div>
      <div class="col2" :class="{'signup-form':!showLoginForm}">
        <form @submit.prevent v-if="showLoginForm">
          <h1>Welcome Back</h1>
          <div>
            <label for="email1">Email</label>
            <input
              v-model.trim="loginForm.email"
              type="text"
              placeholder="you@email.com"
              id="email1"
            />
          </div>
          <div>
            <label for="password1">Password</label>
            <input
              v-model.trim="loginForm.password"
              type="password"
              placeholder="******"
              id="password1"
            />
          </div>
          <button class="button" @click="login">Log In</button>
          <div class="extras">
            <a @click="togglePasswordReset">Forgot Password</a>
            <a @click="toggleForm">Create an Account</a>
          </div>
        </form>
        <form @submit.prevent v-else>
          <h1>Get Started</h1>
          <div>
            <label for="name">Name</label>
            <input
              v-model.trim="signupForm.name"
              type="text"
              placeholder="Savvy Apps"
              id="name"
            />
          </div>
          <div>
            <label for="title">Title</label>
            <input
              v-model.trim="signupForm.title"
              type="text"
              placeholder="Company"
              id="title"
            />
          </div>
          <div>
            <label for="email2">Email</label>
            <input
              v-model.trim="signupForm.email"
              type="text"
              placeholder="you@email.com"
              id="email2"
            />
          </div>
          <div>
            <label for="password2">Password</label>
            <input
              v-model.trim="signupForm.password"
              type="password"
              placeholder="min 6 characters"
              id="password2"
            />
          </div>
          <button @click="signup()" class="button">Sign Up</button>
          <div class="extras">
            <a @click="toggleForm">Back to Log In</a>
          </div>
        </form>
        <hr>
      
        <div class="">
          <router-link to="/suspense">Go To Suspense</router-link>
        </div>
        <div class="">
          <WatcherExample />

        </div>
        
      </div>
    </section>
  </div>
</template>

<script>
import PasswordReset from "../components/PasswordReset";
import {computed, ref} from "@vue/reactivity";
import WatcherExample from "./watcher/WatcherExample";

export default {
  components: {
    PasswordReset,
    WatcherExample
  },
  data: function() {
    return {
      loginForm: {
        email: "",
        password: ""
      },
      // add signup form to data()
      signupForm: {
        name: "",
        title: "",
        email: "",
        password: ""
      },
      showLoginForm: true,
      showPasswordReset: false
    };
  },
  methods: {
    login() {
      this.$store.dispatch("login", {
        email: this.loginForm.email,
        password: this.loginForm.password
      });
    },
    signup() {
      this.$store.dispatch("signup", {
        email: this.signupForm.email,
        password: this.signupForm.password,
        name: this.signupForm.name,
        title: this.signupForm.title
      });
    },
    toggleForm() {
      this.showLoginForm = !this.showLoginForm;
    },
    togglePasswordReset() {
      this.showPasswordReset = !this.showPasswordReset;
    }
  },
  setup() {
    let formName = ref('');
    let formEmail = ref('');

    return {
      formName,
      formEmail
    }
  }
};
</script>

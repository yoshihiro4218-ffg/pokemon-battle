<template>
  <div class="loginDiv">
    <h2>LoginForm!!</h2>
    <router-link id="new-user" class="routerLink" to="/userRegisterForm">
      未登録の方はこちらでユーザ登録をしてください<br>
    </router-link>

    <form name="loginForm">
      <div class="form-group">
        <label for="email">Email address</label>
        <input type="email" class="form-control" id="email" aria-describedby="emailHelp"
               placeholder="Enter email" name="email">
        <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone
          else.</small>
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input type="password" class="form-control" id="password"
               placeholder="Password" name="password">
      </div>
      <div class="form-group form-check" style="display: none;">
        <input type="checkbox" class="form-check-input" id="exampleCheck1">
        <label class="form-check-label" for="exampleCheck1">Check me out</label>
      </div>
      <button type="button" class="btn btn-primary" v-on:click="login">ログイン</button>
    </form>
  </div>
</template>

<script>
  import axios from 'axios'
  import store from '../store/index.js'
  import {mapState} from 'vuex'

  export default {
    name: "Login",
    data() {
      return {
        items: [],
        csrf: "",
      }
    },
    components: {},
    computed: {},
    watch: {
      items() {
      }
    },
    mounted() {
      // TODO: csrf対策を一時的にoffにしているのでコメントアウト
      // axios.get("/api/prelogin")
      //     .then((res) => {
      //         console.log(res.data);
      //         this.csrf = res.data;
      //     })
    },
    methods: {
      login() {
        let params = new URLSearchParams();
        params.append('email', document.getElementById("email").value);
        params.append('pass', document.getElementById("password").value);
        // TODO: csrf対策を一時的にoffにしているのでコメントアウト
        // params.append('_csrf', this.csrf);
        console.log(document.getElementById("email").value);
        console.log(this.csrf);
        console.log(params);
        axios.post("/api/login", params).then((res) => {
          console.log(res)
          this.$router.push("/trainerList")

        });
      }
    }
  }
</script>

<style scoped>
  .loginDiv {
    text-align: center;
    position: relative;
    display: block;
    box-sizing: border-box;
    margin-right: auto;
    margin-left: auto;
  }

  form {
    text-align: center;
  }

  .form-group {
    margin-right: auto;
    margin-left: auto;
    width: 500px;
    text-align: center;
  }

</style>
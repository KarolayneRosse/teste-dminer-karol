<template>
  <div class="home">
    <div v-show="!logged">
      <b-form-group>
        <b-form-input
          v-model="value"
          class="input ml-5"
          placeholder="Insira uma frase aqui:"
        ></b-form-input>
      </b-form-group>
      <p class="changeColor">{{ inputValue }}</p>
    </div>
    <div v-show="logged">
      <h3>Usuário logado no momento</h3>
      <br>
      <p>Nome: {{user.login}}</p>
      <p>Nome: {{user.usuario}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      value: "",
      user:{}
    };
  },
  computed: {
    inputValue() {
      return this.value.split("").reverse().join("");
    },
    logged(){
      return this.$store.state.loggedIn
    },
  },
  created(){
    this.getUserData()
  },
  methods: {
    getUserData(){
      if (this.$store.state.loggedIn) {
        this.$http.get('https://www.dminerweb.com.br:8553/api/auth_user')
        .then(res =>{
          this.user = res.data
        })
      }
    }
  },
};
</script>
<style scoped>
.input {
  width: 350px;
}
.changeColor {
  color: red;
}
</style>
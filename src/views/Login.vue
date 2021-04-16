<template>
  <div id="login">
    <b-card class="cartao">
      <b-form>
        <b-form-group label="Nome">
          <b-input-group>
            <b-form-input type="text" v-model="form.userName" class="border-dark"></b-form-input>
          </b-input-group>
        </b-form-group>

        <b-form-group label="Senha">
          <b-input-group>
            <b-form-input
              type="text"
              v-model="form.userPassword"
            ></b-form-input>
          </b-input-group>
        </b-form-group>
      </b-form>
      <b-button @click="submit()">{{ btnReq }}</b-button> 
    </b-card>
  </div>
</template>
<script>
export default {
  data() {
    return {
      form: {
        userName: "",
        userPassword: "",
      },
      btnReq: "Enviar",
      load: false,
    };
  },
  methods: {
    submit() {
      if (!this.load) {
        this.load = true;
        this.btnReq = 'Enviando...'

        this.$http
          .post("https://www.dminerweb.com.br:8553/api/auth", this.form)
          .then((res) => {
              this.btnReq = 'Enviar'
            console.log(res.data);
            this.load = false
            //   this.$store.state.loggedIn = true;
            //this.$store.state.user = res.data
            //   this.$router.push("/");
          }, error =>{
              this.btnReq = 'Enviar'
              console.error(error.data);
          });
      }
    },
  },
};
</script>
<style scoped>
#login {
  display: flex;
  align-items: center;
  justify-content: center;
}
.cartao {
  width: 600px;
}
</style>
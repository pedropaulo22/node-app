<script>
import axios from "axios";

export default {
  layout: "externo",
  data() {
    return {
      usuario: {
        fullname: null,
        password: null,
        email: null
      }
    };
  },
  methods: {
    async registrar() {
      try {
        axios
          .post("http://localhost:3001/", this.usuario)
          .then(r => console.log(r));

        this.$router.push("/login");
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>

<template>
  <div>
    <h1>Notes App</h1>
    <p>Informe os dados abaixo para se registrar</p>

    <b-form @submit.prevent="registrar">
      <b-form-group>
        <b-form-input
          v-model="usuario.fullname"
          type="text"
          placeholder="Nome"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group>
        <b-form-input
          v-model="usuario.email"
          type="email"
          placeholder="E-mail"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group>
        <b-form-input
          v-model="usuario.password"
          type="password"
          placeholder="Senha"
          required
        ></b-form-input>
      </b-form-group>

      <b-button v-if="$nuxt.isOnline" block type="submit" variant="primary"
        >Registrar</b-button
      >

      <b-button class="mt-5" to="login" block variant="link">Acessar</b-button>
    </b-form>
  </div>
</template>

<style></style>

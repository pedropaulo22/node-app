<script>
import axios from "axios";

export default {
  layout: "externo",
  data() {
    return {
      usuario: {
        password: null,
        email: null
      }
    };
  },
  methods: {
    async login() {
      try {
        await axios
          .get(`http://localhost:3001/logon/${this.usuario.email}`)
          .then(r => console.log(r));

        this.$router.push("/nota/new");
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

    <b-form @submit.prevent="login">
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
        >Acessar</b-button
      >

      <b-button class="mt-5" to="registro" block variant="link"
        >registrar</b-button
      >
    </b-form>
  </div>
</template>

<style></style>

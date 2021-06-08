<template>
  <div>
    <b-navbar type="dark" variant="dark">
      <b-navbar-brand href="/">Notes App</b-navbar-brand>
      <b-navbar-toggle target="notesBar"></b-navbar-toggle>

      <b-collapse id="notesBar" is-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown :text="primeiroNome" right>
            <b-dropdown-item href="perfil">Perfil</b-dropdown-item>
            <b-dropdown-item href="#" @click.prevent="logout"
              >Sair</b-dropdown-item
            >
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>

    <div class="container">
      <div class="card bg-warning my-5">
        <div class="card-body">
          <b-form @submit.prevent="buscar" autocomplete="off">
            <b-form-group>
              <b-form-input
                class="bg-warning border-0 titulo text-dark"
                type="text"
                size="lg"
                placeholder="Tag"
                v-model="info.tag"
              ></b-form-input>
              <b-button
                v-if="$nuxt.isOnline"
                block
                type="submit"
                variant="primary"
                >Buscar</b-button
              >
            </b-form-group>
            <div>
              {{ info.tagValue }}
            </div>
          </b-form>
        </div>
      </div>
      <offline-alert v-show="$nuxt.isOffline" />

      <Nuxt />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      info: {
        tag: null,
        tagValue: ""
      }
    };
  },
  methods: {
    async buscar() {
      try {
        await axios
          .get(`http://localhost:3001/tag/${this.info.tag}`)
          .then(r => (this.info.tagValue = r.data[0].description));
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>

<style></style>

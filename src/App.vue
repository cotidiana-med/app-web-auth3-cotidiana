<template>
  <div id="app">
    <head>
      <title>Auth</title>
      <link
        href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700|Material+Icons"
        rel="stylesheet">
    </head>
    <v-app>
      <v-content>
        <v-container>
          <img
            :src="logoSrcUrl"
            height="50px">
          <router-view/>
          <span><b>{{ ctx.accessState.basePatientId }}</b></span>
        </v-container>
      </v-content>
    </v-app>
  </div>
</template>

<script>
import Context from './context.js';

export default {
  name: 'App',
  data: () => ({
    title: 'App-web-auth3',
    logoSrcUrl: null,
  }),
  errorCaptured (err, vm, info) {
    alert(`[Vue warn]: Unexpected error in ${info}:
      ${err}`);
  },
  async created () {
    this.ctx = new Context(this.$route.query);
    await this.ctx.init();
    const assets = await this.ctx.pryvService.assets();
    assets.setAllDefaults();
    this.logoSrcUrl =
      assets.relativeURL(assets._assets['app-web-auth3'].logo.url);
  },
};
</script>

<style>
  #app {
      font-family: 'Roboto', 'Avenir', Helvetica, Arial, sans-serif;
      text-align: center;
      padding-left: 20px;
      padding-right: 20px;
  }
  h3 {
    margin: 8px;
    display: inline;
  }
</style>

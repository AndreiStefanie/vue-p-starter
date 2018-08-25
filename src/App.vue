<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>

<script>
import { loadLanguageAsync } from './i18n';

export default {
  metaInfo() {
    return {
      // if no subcomponents specify a metaInfo.title, this title will be used
      title: 'Vue-P-Starter',
      // all titles will be injected into this template
      titleTemplate: '%s | Vue-P-Starter',
      htmlAttrs: {
        lang: this.$i18n.locale || 'en',
        amp: undefined // "amp" has no value
      }
    };
  },
  created() {
    this.setupLocale();
  },
  methods: {
    setupLocale() {
      loadLanguageAsync(this.$cookies.lang || 'en');
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: $vueColor;
    }
  }
}
</style>

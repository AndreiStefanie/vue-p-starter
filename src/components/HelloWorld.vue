<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank">vue-cli documentation</a>.
    </p>
    <div v-if="$store.getters['links/hasLinks']">
      <h3>Installed CLI Plugins</h3>
      <ul>
        <li v-for="p in plugins" :key="p.name">
          <a :href="p.link" target="_blank">{{ p.name }}</a>
        </li>
      </ul>
      <h3>Essential Links</h3>
      <ul>
        <li v-for="e in essentials" :key="e.name">
          <a :href="e.link" target="_blank">{{ e.name }}</a>
        </li>
      </ul>
      <h3>Ecosystem</h3>
      <ul>
        <li v-for="es in ecosystem" :key="es.name">
          <a :href="es.link" target="_blank">{{ es.name }}</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import linksService from '@/services/LinksService';
import { mapActions, mapState } from 'vuex';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {};
  },
  created() {
    this.getLinks().then(links => {
      // Store the retrieved links in the Vuex state
      this.setLinks(links);
    });
  },
  computed: {
    ...mapState('links', ['plugins', 'essentials', 'ecosystem'])
  },
  methods: {
    async getLinks() {
      const plugins = await linksService.getPlugins();
      const essentials = await linksService.getEssentials();
      const ecosystem = await linksService.getEcosystem();
      return {
        plugins,
        essentials,
        ecosystem
      };
    },
    ...mapActions({
      setLinks: 'links/setLinks'
    })
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  // Notice we can use scss variables defined in the loaded scss files
  color: $vueColor;
}
</style>

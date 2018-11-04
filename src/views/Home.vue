<template>
  <div class="home">
    <img src="../assets/logo.png" alt="">
    <HelloWorld :msg="$t('greeting')"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';

export default {
  name: 'home',
  components: {
    HelloWorld
  },
  metaInfo: {
    title: 'Home Page'
  }
};
</script>

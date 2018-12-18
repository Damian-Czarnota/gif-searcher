<template>
  <div id="app">
    <GifSearcher />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import GifSearcher from './containers/GifSearcher.vue';

@Component({
  components: {
    GifSearcher,
  },
})
export default class App extends Vue {}
</script>

<style lang="scss">
@import './styles.scss';
</style>

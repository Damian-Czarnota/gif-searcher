<template>
  <div>
    <Searcher @change-gif-name="getGifs"/>
    <h1>{{ gifName }}</h1>
    <Favorites />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import Favorites from '../components/Favorites.vue';
import Searcher from '../components/Searcher.vue';

@Component({
  components: {
    Favorites,
    Searcher,
  },
})
export default class GifSearcher extends Vue {
  private gifName: string = '';
}
</script>


<style scoped lang="scss">

</style>

<template>
  <div>
    <Searcher @change-gif-name="getGifsComponent"/>
    <h1>{{ gifName }}</h1>
    <Favorites />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import Favorites from '../components/Favorites.vue';
import Searcher from '../components/Searcher.vue';
import DataService from '../services/DataService.vue';

@Component({
  components: {
    Favorites,
    Searcher,
  },
})
export default class GifSearcher extends Vue {
  private gifName: string = '';
  private gifsArray: Array<[]> = [];
  private getGifsComponent(gifName: string) {
    DataService.getGifs(gifName).then(
            ({data}) => {
              this.gifsArray = data.data;
            },
            (error) => {
                alert('Something went wrong... Try again later');
            });
  }
}
</script>


<style scoped lang="scss">

</style>

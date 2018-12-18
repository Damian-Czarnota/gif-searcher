<template>
  <div>
    <Searcher @change-gif-name="getGifsComponent"/>
    <h1>Results</h1>
    <Grid :config="config" :data="gifsArray" @add-to-favorite="addToFavorites" @remove-from-favorite="removeFromFavorites"/>
    <h1>Favorites</h1>
    <Grid :config="config" :data="favoritesArray" @add-to-favorite="addToFavorites" @remove-from-favorite="removeFromFavorites"/>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import Searcher from '../components/Searcher.vue';
import DataService from '../services/DataService.vue';
import Grid from '../components/Grid.vue';

@Component({
  components: {
    Searcher,
    Grid,
  },
})
export default class GifSearcher extends Vue {
  private gifName: string = '';
  private gifsArray: Array<{}> = [];
  private favoritesArray: List<{}> = [];
  private config: Array<{}> = [
  { key: 'image_url', title: 'Gif', type: 'image' },
  { key: 'bitly_gif_url', title: 'URL', type: 'code' },
  { key: 'title', title: 'Title', type: 'text' },
  { key: 'favorite', title: 'Favorite', type: 'favorite' },
  ];
  private getGifsComponent(gifName: string) {
    DataService.getGifs(gifName).then(
            ({data}) => {
              this.gifsArray = data.data;
              this.gifsArray.forEach((item: any, index) => {
                this.gifsArray[index].image_url = item.images.fixed_height.url;
                this.gifsArray[index].favorite = false;
              });
            },
            (error) => {
                alert('Something went wrong... Try again later');
            });
  }
  //@TODO
  private addToFavorites(item: object) {
      item.favorite=!item.favorite;
      this.favoritesArray.push(item);
  }

  //@TODO
  private removeFromFavorites(item: object) {
    item.favorite=!item.favorite;
    this.favoritesArray = this.favoritesArray.filter((el: any) =>{
              return el!=item;
            });
  }
}
</script>


<style scoped lang="scss">

</style>

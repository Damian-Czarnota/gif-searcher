<template>
  <div>
    <Searcher @change-gif-name="getGifsComponent"/>
      <div class="header-center">
          <h1>Results</h1>
      </div>
    <Grid v-if="gifsArray.length>0" :config="config" :data="gifsArray" @add-to-favorite="addToFavorites" @remove-from-favorite="removeFromFavorites"/>
      <div v-if="gifsArray.length===0" class="empty-info">
          <i class="far fa-images"></i>
          <p>There is no data.</p>
          <p>Start form searching or change parameters</p>
      </div>
      <div class="header-center">
        <h1>Favorites</h1>
    </div>
    <Grid v-if="favoritesArray.length>0" :config="config" :data="favoritesArray" @add-to-favorite="addToFavorites" @remove-from-favorite="removeFromFavorites"/>
      <div v-if="favoritesArray.length===0" class="empty-info">
          <i class="fas fa-star"></i>
          <p>There is no data.</p>
          <p>Start adding gifs to favorites</p>
      </div>
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
  private favoritesArray: Array<{}> = [];
  private config: Array<{}> = [
  { key: 'image_url', title: 'Gif', type: 'image' },
  { key: 'bitly_gif_url', title: 'URL', type: 'code' },
  { key: 'title', title: 'Title', type: 'text' },
  { key: 'favorite', title: 'Favorite', type: 'favorite' },
  ];
    constructor(){
        super();
        if(sessionStorage.getItem('favoritesArray'))
            this.favoritesArray = JSON.parse(sessionStorage.getItem('favoritesArray'));
    }
  private getGifsComponent(gifName: string) {
    DataService.getGifs(gifName).then(
            ({data}) => {
              this.gifsArray = data.data;
              this.gifsArray.forEach((item: any, index) => {
                this.gifsArray[index].image_url = item.images.fixed_height.url;
                if(this.favoritesArray)
                        this.favoritesArray.forEach(el =>{
                            if(el.id===this.gifsArray[index].id)
                                this.gifsArray[index].favorite = el.favorite;
                        })
              });
            },
            (error) => {
                alert('Something went wrong... Try again later');
            });
  }
  private addToFavorites(item: any) {
      item.favorite=!item.favorite;
      Vue.set(this.gifsArray,this.gifsArray.indexOf(item), {...item,favorite:item.favorite})
      this.favoritesArray.push(item);
      sessionStorage.setItem('favoritesArray',JSON.stringify(this.favoritesArray));
  }
  private removeFromFavorites(item: any) {
    item.favorite=!item.favorite;
      this.gifsArray.forEach(el =>{
          if(el.id===item.id)
            el.favorite=item.favorite;
      });
    this.favoritesArray = this.favoritesArray.filter((el: any) =>{
            if(el.id!=item.id)
              return el;
            });
    sessionStorage.setItem('favoritesArray',JSON.stringify(this.favoritesArray));
  }
}
</script>


<style scoped lang="scss">

</style>

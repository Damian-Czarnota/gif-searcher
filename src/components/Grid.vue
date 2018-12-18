<template>
  <div>
    <table class="table">
      <thead>
      <tr>
        <th class="table__header" v-for="key in config">
          {{key.title}}
        </th>
        <th>

        </th>
      </tr>
      </thead>
      <tbody>
       <tr v-for="item in data" class="table__row">
         <td v-for="row in config" class="table__cell">
           <img :src=item[row.key] v-if="row.type==='image'" style="width:256px;height:128px">
           <span v-if="row.type==='code'">{{item[row.key]}}</span>
           <button v-if="row.type==='favorite'" class="favorite-button"><i v-if="!item[row.key]" class="far fa-star" @click="addToFavorite(item)"></i>
             <i v-if="item[row.key]" class="fas fa-star" @click="removeFromFavorite(item)"></i>
           </button>
         </td>
       </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Grid extends Vue {
  @Prop() private config!: Array<[]>;
  @Prop() private data!: Array<[]>;

  private addToFavorite(item: object) {
    this.$emit('add-to-favorite', item);
  }
  private removeFromFavorite(item: object) {
    this.$emit('remove-from-favorite', item);
  }
}
</script>


<style scoped lang="scss">

</style>

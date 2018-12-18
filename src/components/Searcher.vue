<template>
  <div id="searcher">
    <div class="form">
    <div class="control_input">
      <input name="gifName" v-model="gifName" type="text" class="custom_input" required />
      <label class="custom_label">Search Your gifs</label>
    </div>
      <button class="custom_button" v-on:click="sendGifName">Search</button>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Searcher extends Vue {
  private gifName: string = '';
  private sendGifName(){
    this.$emit('change-gif-name', this.gifName);
  }
}
</script>


<style scoped lang="scss">
#searcher{
  width:100%;
  display: flex;
  justify-content: center;
}

  .form{
    width:50%;
  }
</style>

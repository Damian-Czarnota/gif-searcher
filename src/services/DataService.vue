<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import axios from 'axios';

@Component({})
export default class DataService extends Vue {
  public static API_KEY: string = 'EwQCHDTYU2onchg4pwYQmRFRcugz5ySa';
  public static API_URL: string = 'http://api.giphy.com/v1';
  public static $axios = axios;

  public static getGifs(param: string) {
    return this.$axios.get(`${this.API_URL}/gifs/search?q=${param}&api_key=${this.API_KEY}&limit=5`);
  }
}
</script>


<style scoped lang="scss">

</style>

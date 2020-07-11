<template>
  <div class="row">
  <div class="col-sm-3">
    <div class="card" v-for="title in titles" :key="title.id" :id="title.id" title="title.title">
        <img :src="'https://www.dailymotion.com/thumbnail/video/'+title.id" alt="" class="card-img-top"> 
      <div class="card-body">
        <h5 class="card-title">{{ title.title }}</h5>
        <a v-bind:href="'https://www.dailymotion.com/video/'+title.id" class="btn btn-primary">Play</a>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import axios from "axios";
export default {
  props: ['title', 'id'],
  components: {
   
  },
  data() {
    return {
      titles: []
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get("https://api.dailymotion.com/videos?channel=news&limit=10", config);
      this.titles = res.data.list;
    } catch(err) {
      console.log(err);
    }
  },
}
</script>

<style>


</style>

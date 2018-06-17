<template>
    <aplayer v-if='loadSuccess' :autoplay='true' :showLrc='true' :music="musicList[0]" :list='musicList'></aplayer>
</template>

<script>
import Aplayer from "vue-aplayer";
import axios from "axios";
export default {
  components: {
    Aplayer
  },
  data() {
    return {
      musicList: [],
      loadSuccess: false
    };
  },
  created() {
    axios.get("/static/data/musicdata.json").then(res => {
      console.log(res)
      res.data.musicData.forEach(element => {
        
        this.musicList.push({
          title: element.title,
          artist: element.author,
          src: element.src,
          pic: element.musicImgSrc,
          lrc: '/static/' + element.lrc
        });
      });
      this.loadSuccess = true;
      
    });
  }
};
</script>

<style scoped>
.aplayer{
    margin-top: 1rem;
}
</style>

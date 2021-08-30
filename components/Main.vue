<template lang="pug">
  div
    AppHeader
    .container
      .video-list
        VideoCard(
          v-for="item in videoData"
          :itemData="item"
        )
    AppFooter
</template>
<script>
import axios from 'axios';

export default {
  name: 'Main',
  data () {
    return {
      videoData: [],
    }
  },
  created() {
    const base = 'https://www.googleapis.com/youtube/v3/videos?part=contentDetails,snippet';
    const key = 'AIzaSyDWvlhjOKLPAbP1SP1HUT14hgsy7XfHHxk';

    const url = base;
    const params = { 
      key,
      chart: 'mostPopular',
      regionCode: 'TW',
      maxResults: '24',
      videoCategoryId: 0
    };

    axios.get(url, { params })
      .then(res =>{
          this.videoData = res.data.items;
      }).catch(err => {
          console.log(err);
      })
  },
}
</script>
<style lang="scss">
.container {
  padding: 96px 0 48px 0;

  .video-list {
    @include Flex(center, flex-start);

    flex-wrap: wrap;
  }
}
</style>

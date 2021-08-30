<template lang="pug">
.video-card
  .card-img(:style="{ backgroundImage: `url(${videoInfo.image})`}")
  .card-content
    img.channel-img(src="http://fakeimg.pl/300/")
    a
      .title {{videoInfo.title}}
      .channel-title {{videoInfo.channelTitle}}
</template>
<script>
export default {
  data () {
    return {
      videoInfo: {},
    }
  },
  created() {
    this.videoInfo = this.getVideoCardFormat(this.itemData);
  },
  props: ["itemData"],
  methods: {
    getVideoCardFormat(itemData) {
      const { snippet, id } = itemData;
      const{ thumbnails, title, description, channelTitle } = snippet;
      let image = thumbnails;
      image =
        image.maxres ||
        image.standard ||
        image.height ||
        image.medium ||
        image.default;
      return {
        id,
        title,
        description,
        image: image.url,
        channelTitle
      };
    }
  }
}
</script>
<style lang="scss">
.video-card {
  width: calc(25% - (8px*2));
  margin: 0 8px;
  cursor: pointer;

  @include pc-width {
    width: calc(33.3% - (8px*2));
  }

  @include phone-width {
    width: calc(50% - (8px*2));
  }

  @include iphone-width {
    width: calc(100% - (8px*2));
  }

  .card-img {
    max-width: 460px;
    max-height: 259px;
    padding-bottom: 56.25%;
    position: relative;
    overflow: hidden;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;

    @include iphone-width {
      max-width: 100%;
    }
  }

  > .card-content {
    @include Flex(space-around);
    margin-top: 4px;
    margin-bottom: 24px;
    font-size: 14px;

    .channel-img {
      @include size(40px);
      @include BrdRad(50%);
      margin-right: 12px;
    }

    .title, .channel-title {
      max-height: 35px;
      overflow: hidden;
      line-height: 1.25;
      text-overflow: ellipsis;
    }

    .channel-title {
      opacity: .6;
    }
  }
}
</style>

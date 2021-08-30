<template lang="pug">
#footer.footer
  NuxtLink.panel-btn(
    v-for="item in panelData"
    :to="item.link"
    :class="$route.path !== item.link ? ' inactive ' : ''"
    )
      i.material-icons {{item.icon}}
      p {{item.name}}
</template>
<script>
export default {
  data () {
    return {
      panelData: [
        {
          name: '首頁',
          icon: 'home',
          link: '/',
        },
        {
          name: '發燒影片',
          icon: 'local_fire_department',
          link: '/hot',
        },
        {
          name: '訂閱內容',
          icon: 'subscriptions',
          link: '/subscribe',
        },
        {
          name: '媒體庫',
          icon: 'playlist_play',
          link: '/media',
        },
      ]
    }
  },
}
</script>
<style lang="scss">
#footer {
  @include Flex();
  @include Bgc($c1);
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 48px;
  z-index: 120;
  border-top: 1px solid rgba(0,0,0,0.102);

  > .panel-btn {
    flex: 1;
    text-align: center;

    p {
      @include ellipsis();
      font-size: 12px;
    }

    &.inactive {
      color: rgba(0, 0, 0, 0.26); 
    }
  }
}

</style>

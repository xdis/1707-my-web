<template>
  <div id="app">
    <transition name="side">
      <side-menu v-show="show" @hide="hideSide"></side-menu>
    </transition>
    <router-view/>
  </div>
</template>

<script>
import SideMenu from './components/SideMenu1'
import bus from './bus'
export default {
  name: 'app',
  components: {
    SideMenu
  },
  created () {
    this.$http.get(`/douyuapi/RoomApi/live?offset=1&limit=20`).then(res => {
      console.log(res.data.data)
    })
  },
  data () {
    return {
      show: false
    }
  },
  mounted () {
    bus.$on('showSide', this.side)
  },
  methods: {
    side () {
      this.show = !this.show
    },
    hideSide () {
      this.show = false
    }
  }
}
</script>

<style>
  .side-enter-active,.side-leave-active,
  .side-enter-active ul,.side-leave-active ul{
    transition:all .4s linear;
  }
  .side-enter,.side-leave-active{
    opacity: 0;
  }
  .side-enter ul,.side-leave-active ul{
    transform:translateX(-50%);
    opacity:0;
  }
</style>

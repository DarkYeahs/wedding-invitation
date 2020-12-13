<template>
  <div id="app">
    <audio
      v-if="isPlay"
      loop="true"
      :src="bgm" ></audio>
    <img src="@/assets/bg.png" alt="">
    <div class="shadow">
      <div class="stars">
          <div class="star"></div>
          <div
            v-for="i in 39"
            :key="i"
            :class="`star${i}`"
            class="star"></div>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import bgm from '@/assets/bgm.mp3'

export default {
  name: 'App',
  data: () => ({
    element: null,
    bgm,
    isPlay: false
  }),
  mounted () {
    setTimeout(() => {
      this.isPlay = true
    }, 200)
    setTimeout(() => {
      this.init()
    }, 400)
  },
  methods: {
    init () {
      this.element = this.$el.querySelector('audio')
      this.play()
      document.addEventListener('touchstart', this.play, false)
      document.addEventListener('WeixinJSBridgeReady', () => { this.play('WeixinJSBridgeReady') }, false)
    },

    play (str = 'touchstart') {
      console.log('play', str)
      if (this.element) {
        try {
          console.log('element', this.element)
          this.element.play()
            .catch(e => {
              console.log(e)
            })
        } catch (e) {
          console.log(e)
        }
      }
    }
  },
  components: {
    HelloWorld
  }
}
</script>

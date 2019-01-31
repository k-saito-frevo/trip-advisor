<template>
  <section class="container">
    <div>
      <!-- <logo/> -->
      <div id="video-background">
        <div id="video">
          <video :src="movieSrc" muted="true" autoplay="true" controls="" loop="true"/>
          <!-- <iframe src="https://www.youtube.com/embed/tPjatq3A8TI?controls=0&amp;start=21&autoplay=1&rel=0&modestbranding=1&disablekb=0&showinfo=0&fs=0&controls=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe> -->
        </div>
      </div>
    </div>
    <div>
      <p class="subtitle">Where is next destination?</p>
    <!-- <nuxt-link to="/shootPic"> -->
        <!-- <p>写真撮影画面</p> -->
        <button class="button is-success front" @click="$router.push('shootPic')">Choose it!</button>
    <!-- </nuxt-link> -->
    </div>
  </section>
</template>

<script>
import axios from 'axios'
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  created(){
    const self = this 
    let movieArr = []
    movieArr.push(require("../static/test.mp4"))
    movieArr.push(require("../static/test2.mp4"))
    movieArr.push(require("../static/test3.mp4"))
    movieArr.push(require("../static/test4.mp4"))
    movieArr.push(require("../static/test5.mp4"))
    self.movieSrc = movieArr[Math.floor(Math.random() * movieArr.length)]
  },
  data(){
    return{
      movieSrc:""
    }
  }
}
</script>

<style>
* {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
}

#video-background {
  background: #000;
  position: fixed;
  top: 0; right: 0; bottom: 0; left: 0;
  z-index: -99;
}
 #video,#video-background iframe,#video-background video{
  top: 0; right: 0; bottom: 0; left: 0;
  opacity:0.7;
  position: absolute;
  min-width: 100%;
  min-height: 100%;
  pointer-events: none;
  z-index: -96;
}

.front{
  z-index:1;
}
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-size: 2em;
  color: #F0F0F0;
  word-spacing: 10px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

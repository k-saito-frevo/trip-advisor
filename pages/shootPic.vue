<template>
<section class="hero is-primary">
  <div class="hero-body">
    <button class="button is-link" v-on:click="startVideo">
      <i class="material-icons">start</i>
      <i class="fab fa-github"></i>
    </button>
    <button class="button is-link" v-on:click="stopVideo">
      <i class="material-icons">stop</i>
      <i class="fab fa-github"></i>
    </button>
    <br />
    <video id="local_video" autoplay></video> 
    <!-- <canvas :id="photoContainer" :value="{{photo}}"/> -->
  </div>
</section>
</template>
<script>


export default {
    data(){
      return{
        photo:null,
        stream:null
      }
    },
    methods:{
        startVideo:function(event){
            const self = this
            let localVideo = document.getElementById('local_video');
            let localStream;
            navigator.mediaDevices.getUserMedia({video: true, audio: false})
            .then(function (stream) { // success
              localStream = stream;
              self.stream = localStream
              localVideo.src = window.URL.createObjectURL(self.stream);
            }).catch(function (error) { // error
              console.error('mediaDevice.getUserMedia() error:', error);
              return;
            })
        },
        takePhoto:function(event){

        },
        stopVideo:function(event){
          if (null !== self.stream){
            const self = this
            self.stream.getTracks().forEach(track => track.stop());

          }
        }
    }
}
</script>

<style>
  #local_video{
    width:100%;
    height:100%;
    opacity:0.8;
  }
</style>

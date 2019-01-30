<template>
<section class="hero is-primary">
  <div class="hero-body">
    <button class="button is-link" @click="startVideo">
      <i class="material-icons">start</i>
      <i class="fab fa-github"></i>
    </button>
    <button class="button is-danger" @click="stopVideo">
      <i class="material-icons">stop</i>
      <i class="fab fa-github"></i>
    </button>
    <button class="button is-info" @click="takePhoto" >
      shoot
    </button>
    <button class="button is-success" @click="submit" >
      submit
    </button>
    <br />
    <video id="local_video" autoplay></video> 
    <canvas id="photoContainer" />
    <img id="photo">
  </div>
</section>
</template>
<script>

import CONSTANTS from '../assets/constants.js'
export default {
    data(){
      return{
        photo:null,
        stream:null,
        usedFlg:false
      }
    },
    methods:{
        startVideo(){
            const self = this
            let localVideo = document.getElementById('local_video');
            if(self.usedFlg) return
            navigator.mediaDevices.getUserMedia({video: true, audio: false})
            .then(function (stream) { // success
              self.usedFlg = true
              self.stream = stream
              localVideo.srcObject = self.stream
            }).catch(function (error) { // error
              console.error('mediaDevice.getUserMedia() error:', error)
              return
            })
        },
        takePhoto(){
          if(!this.usedFlg) return
          let video  = document.getElementById('local_video')
          let canvas = document.getElementById('photoContainer')
			    let img = document.getElementById('photo')

          let ctx = canvas.getContext('2d')
			    //videoの縦幅横幅を取得
			    let w = video.offsetWidth
			    let h = video.offsetHeight

			    //同じサイズをcanvasに指定
			    canvas.setAttribute("width", w)
			    canvas.setAttribute("height", h)

			    //canvasにコピー
			    ctx.drawImage(video, 0, 0, w, h)
			    //imgにpng形式で書き出し
          img.src = canvas.toDataURL('image/png')
          ctx.clearRect(0, 0, w, h)     
               
        },
        stopVideo(){
          if (null !== self.stream){
            const self = this
            self.usedFlg = false
            self.stream.getTracks().forEach(track => track.stop())

          }
        },
        async submit(){
          let imgSrc = document.getElementById("photo").src        
          const self = this
          try{
            let headers = {headers:{"Access-Control-Allow-Origin":"*"}}
            // console.log(headers)
            //let response = await self.$axios.$post(self.createURL(CONSTANTS.API_URL,self.createParam(imgSrc)),headers)
            self.$axios.baseURL = CONSTANTS.API_URL
            console.log(self.$axios)
            console.log(imgSrc)
            let response = await self.$axios.$post(CONSTANTS.API_URL,imgSrc,headers)
            
            console.log(response)
          }catch(error){
            console.log(error)
          }
        },
        createParam(imgSrc){
          return {
            image_file:imgSrc
          }
        },
        judge(response){
          //判定
        },
        createURL(str,arr){
          for(let i=0;i<arr.length;i++){
            str = str.replace(`{${i}}`,arr[i])
          }
          return str
        }
    }
}
</script>

<style>
  #local_video{
    width:60%;
    height:40%;
  }
  
  /* #photo #photo_Container{
    width:400px;
    height:300px;
  } */
</style>

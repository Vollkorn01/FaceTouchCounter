<template>
  <div class="container">
    <div>
      <h1 class="title">VIDEO</h1>
      <!--
      <script
        type="module"
        src="https://cdn.jsdelivr.net/npm/handtrackjs/dist/handtrack.min.js"
      ></script>

      <img
        id="img"
        src="https://bilder.t-online.de/b/86/55/36/76/id_86553676/610/tid_da/frau-fasst-an-ihre-hand-wiederholtes-kribbeln-in-der-hand-sollte-vom-arzt-untersucht-werden-.jpg"
        height="200"
        width="200"
      />
      
      <canvas id="canvas" class="border"></canvas>
      -->
      <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-core"></script>
      <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-converter"></script>
      <script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/handpose"></script>
    </div>
  </div>
</template>

<script>
//import * as handTrack from 'handtrackjs'
import * as handpose from '@tensorflow-models/handpose'
export default {
  components: {},
  mounted: function() {
    // Load the MediaPipe handpose model assets.
    /*
    const img = document.getElementById('img')
    //const canvas = document.getElementById('canvas')
    //const context = canvas.getContext('2d')

    // Load the model.
    handTrack.load().then((model) => {
      // detect objects in the image.
      model.detect(img).then((predictions) => {
        console.log('Predictions: ', predictions)
      })
    })
    */
  },
  methods: {
    async startHandPose() {
      const model = await handpose.load()

      // Pass in a video stream to the model to obtain
      // a prediction from the MediaPipe graph.
      const video = document.querySelector('video')
      const hands = await model.estimateHands(video)

      // Each hand object contains a `landmarks` property,
      // which is an array of 21 3-D landmarks.
      hands.forEach((hand) => console.log(hand.landmarks))
    }
    /*
    startVideo() {
      this.handTrack.startVideo(video).then(function(status) {
        console.log('video started', status)
        if (status) {
          updateNote.innerText = 'Video started. Now tracking'
          isVideo = true
          this.runDetection()
        } else {
          updateNote.innerText = 'Please enable video'
        }
      })
    },

    toggleVideo() {
      if (!isVideo) {
        updateNote.innerText = 'Starting video'
        this.startVideo()
      } else {
        updateNote.innerText = 'Stopping video'
        this.handTrack.stopVideo(video)
        isVideo = false
        updateNote.innerText = 'Video stopped'
      }
    },

    runDetection() {
      model.detect(video).then((predictions) => {
        console.log('Predictions: ', predictions)
        model.renderPredictions(predictions, canvas, context, video)
        if (isVideo) {
          requestAnimationFrame(this.runDetection)
        }
      })
    }
      */
  }
}
</script>

<style>
.container {
  margin: 0 auto;
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
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

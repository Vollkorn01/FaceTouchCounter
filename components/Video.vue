<template>
  <div class="container">
    <div>
      <h1 class="title">VIDEO</h1>
      <!--
      <script
        type="module"
        src="https://cdn.jsdelivr.net/npm/handtrackjs/dist/handtrack.min.js"
      ></script>
-->
      <script type="module">
        import * as handTrack from 'https://cdn.jsdelivr.net/npm/handtrackjs/dist/handtrack.min.js'
      </script>

      <img id="img" src="~assets/hand3.jpg" />

      <canvas id="canvas" class="border"></canvas>

      <!--
      <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-core"></script>
      <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-converter"></script>
      <script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/handpose"></script>
      -->
    </div>

    <body class="bx--body p20">
      <!-- <img id="img" src="hand.jpg"/>  -->
      <div class="p20">
        Handtrack.js allows you prototype handtracking interactions in the
        browser in 10 lines of code.
      </div>
      <div class="mb10">
        <button
          id="trackbutton"
          onclick="toggleVideo()"
          class="bx--btn bx--btn--secondary"
          type="button"
        >
          Toggle Video
        </button>
        <div id="updatenote" class="updatenote mt10">loading model ..</div>
      </div>
      <video
        id="myvideo"
        class="videobox canvasbox"
        autoplay="autoplay"
      ></video>

      <canvas id="canvas" class="border canvasbox"></canvas>

      <script src="https://cdn.jsdelivr.net/npm/handtrackjs/dist/handtrack.min.js"></script>
      <script src="track.js"></script>
    </body>
  </div>
</template>

<script>
//import * as handTrack from 'handtrackjs'
//import * as handpose from '@tensorflow-models/handpose'

export default {
  components: {},
  mounted: function() {
    this.startHandTrack()
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
    /*
    async startHandPose() {
      const model = await handpose.load()

      // Pass in a video stream to the model to obtain
      // a prediction from the MediaPipe graph.
      const video = document.querySelector('video')
      const hands = await model.estimateHands(video)

      // Each hand object contains a `landmarks` property,
      // which is an array of 21 3-D landmarks.
      hands.forEach((hand) => console.log(hand.landmarks))
    },
    */
    startHandTrack() {
      const img = document.getElementById('img')
      const canvas = document.getElementById('canvas')
      // eslint-disable-next-line no-unused-vars
      const context = canvas.getContext('2d')

      // Load the model.
      // eslint-disable-next-line no-undef
      handTrack.load().then((model) => {
        console.log('model: ', model)
        // detect objects in the image.
        console.log('img', img)
        model.detect(img).then((predictions) => {
          console.log('Predictions: ', predictions)
        })
      })
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
body {
  padding: 20px;
}

.p20 {
  padding: 20px;
}

.canvasbox {
  border-radius: 3px;
  margin-right: 10px;
  width: 450px;
  height: 338px;
  border-bottom: 3px solid #0063ff;
  box-shadow: 0 2px 3px 0 rgba(0, 0, 0, 0.2), 0 4px 10px 0 #00000030;
  background: #333;
}

.mb10 {
  margin-bottom: 10px;
}

.mt10 {
  margin-top: 10px;
}

.updatenote {
  padding: 10px;
  background: rgb(245, 147, 20);
  color: white;
  display: inline;
}
</style>

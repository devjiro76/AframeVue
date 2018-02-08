<template>
  <a-scene @click="cameraAutoPlay = !cameraAutoPlay" >
    <a-entity>
      <a-animation
        v-if="cameraAutoPlay"
        attribute="rotation"
        dur="10000"
        fill="both"
        to="0 360 0"
        repeat="indefinite" />
      <a-camera look-controls="reverseMouseDrag: true" />
    </a-entity>

    <a-assets timeout="30000">
      <img
        id="sky"
        :src="skyImage"
        @load="skyLoaded"
        @error="skyErrored" />
    </a-assets>

    <a-sky v-if="skyImageReady" src="#sky" />
    <div v-else>Sky Image is loading ... </div>
  </a-scene>
</template>

<script>
export default {
  data() {
    return {
      cameraAutoPlay: false,
      skyImageReady: false,
      skyImage: "https://upload.wikimedia.org/wikipedia/commons/6/6f/Helvellyn_Striding_Edge_360_Panorama%2C_Lake_District_-_June_09.jpg",
    }
  },

  watch: {
    cameraAutoPlay() {
      console.log('Camera AutoPlay: ', this.cameraAutoPlay)
    }
  },

  methods: {
    skyLoaded() {
      console.log("SKY IMAGE is loaded :D")
      this.skyImageReady = true
    },

    skyErrored(ID) {
      console.error("SKY IMAGE is not loaded")
    }
  }
}
</script>

<style scoped>

</style>

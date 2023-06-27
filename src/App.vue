<template>
  <div id="app">
    <PdfViewer :url="url"/>
  </div>
</template>

<script>
import PdfViewer from './components/PdfViwer/PdfViewer.vue'

export default {
  name: 'App',
  components: {
    PdfViewer
  },

  data() {
    return {
      url: '',
      fileId: '11369802'
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100%;
}

body {
  margin: 0
}
</style>

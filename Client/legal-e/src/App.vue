<template>
  <div id="app">
    buiecuwecuoaij
    <upload-image is="upload-image"
   :url="forms.create.url"
   :max_files="5"
   name="files[]"
   :resize_enabled="true"
   :resize_max_width="640"
   :button_html="forms.create.confirm"
   :button_class="'button is-primary'"
></upload-image>
  </div>
</template>

<script>
import { Web3Storage } from 'web3.storage'
import UploadImage from 'vue-upload-image';
export default {
  name: 'App',
  components: {
    UploadImage,
  },
    mounted(){
  },
  methods : {
    async  storeFiles (files) {
  const client = new Web3Storage("ejkkbwduewbewbcewbewbcewbccwe")
  const cid = await client.put(files)
  console.log('stored files with cid:', cid)
  return cid
}
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

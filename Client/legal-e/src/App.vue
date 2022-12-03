<template>
  <div class="everything">
    nenn
    <button v-on:click="this.showBlocks"> print</button>

    okey this is to upload file

    <input
            type="file"
            name="FILE"
            value=""
            id="FILE"
          /></div>
</template>

<script>
import { Web3Storage } from 'web3.storage'
import { ethers } from "ethers";
export default {
  name: 'App',
  components: {
  },
  data(){
    return{
      provider : undefined,
      fileList : undefined,
      fd : undefined
    }
  },
    mounted(){
      document
      .getElementById("FILE")
      .addEventListener("change", async (event) => {
        this.fileList = event.target.files;
        this.fd = new FormData();
        this.fd.append("image",this.fileList[0]);
        
  })
},
  async created(){
     this.provider = new ethers.providers.Web3Provider(window.ethereum)
    await this.provider.send("eth_requestAccounts", []);
    var dai = require("../../../artifacts/contracts/NFT.sol/MyNFT.json")
    const daiContract = new ethers.Contract("0x5FbDB2315678afecb367f032d93F642f64180aa3", dai.abi, this.provider);
    console.log(daiContract);



   // const signer = provider.getSigner() 
  },
  methods : {
    async  storeFiles (files) {
  const client = new Web3Storage("ejkkbwduewbewbcewbewbcewbccwe")
  const cid = await client.put(files)
  console.log('stored files with cid:', cid)
  return cid
},
  async showBlocks(){
   // var blocks = await this.provider.getBlockNumber()

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

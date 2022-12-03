<template>
  <div id="app">
    <div class="everything">
      <h3>Upload a file</h3>
      <input type="file" name="FILE" value="" id="FILE" hidden />
      <button @click="buttonTrigger()">Upload</button>
    </div>
  </div>
</template>

<script>
import { Web3Storage } from "web3.storage";
 import { ethers } from "ethers";
 //import axios from 'axios'
export default {
  name: 'App',
  components: {
  },
  data(){
    return{
      provider : undefined,
      fileList : undefined,
      fd : undefined,
      daiContract : undefined,
      accounts: undefined,
      sender : undefined,
      account : undefined,
      files : undefined
    }
  },
  mounted() {
    document
      .getElementById("FILE")
      .addEventListener("change", async (event) => {
        this.fileList = event.target.files;
        var fd = new FormData();
        fd.append("image",this.fileList[0]);
        //var response = await axios.post("http://172.17.0.1:5000/post-image")
        // this.files = response.data;
        this.files = fd;
          var cid = this.storeFiles(this.files);
        console.log("https://ipfs.io/ipfs/"+ cid);
        var uri = {
    "name" : "token",
     "URL" : cid,
     "state" : "authentificated"
   }
    await this.daiContract.mintToken(0, JSON.stringify(uri));
  })
},
  async created(){
    //Set Up the WEB 3 Application
    if(typeof window.ethereum !== "undefined") 
    {
      this.accounts = await window.ethereum.request({method:"eth_requestAccounts"})

      this.provider = new ethers.providers.Web3Provider(window.ethereum)
      this.signer = this.provider.getSigner()
      this.account = this.accounts[0]
      var dai = require("../../../artifacts/contracts/NFT.sol/MyNFT.json")
       this.daiContract = new ethers.Contract("0x5FbDB2315678afecb367f032d93F642f64180aa3", dai.abi, this.signer);
    }
    else { 
      console.log("error");
    }




   // const signer = provider.getSigner() 
  },
  methods : {
    // Store the token on the decentrelized IPFS storage
    async  storeFiles (files) {
  const client = new Web3Storage("eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJkaWQ6ZXRocjoweDlEOTFlYjE0NjI0MDI4N2ZhNmQ5RjRhMWNlMDg1NjRmN0E0QTQ2RTkiLCJpc3MiOiJ3ZWIzLXN0b3JhZ2UiLCJpYXQiOjE2NzAwNjU2ODc2MzUsIm5hbWUiOiJmaXJzdCJ9.qdZSqWCi2zwVmfgczfwjZoHgXoJ6ln-8KxRzNLG2-54")
  const cid = await client.put(files)
  console.log('stored files with cid:', cid)
  return cid
},
buttonTrigger() {
      document.getElementById("FILE").click();
    },
    //test
  async showBlocks(){
   // var blocks = await this.provider.getBlockNumber()
   var uri = {
    "name" : "test",
     "URL" : "testurl",
     "state" : "authentificated"
   }
    await this.daiContract.mintToken(0, JSON.stringify(uri));
    var urireturned
    setTimeout(async () => {
          urireturned =  await this.daiContract.tokenURI(0);

    }, 15000);
    console.log(urireturned);
    console.log("object");
  }
  }
}
</script>

<style>
.everything {
  font-family: "Poppins", sans-serif !important;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 200px;
}
h3 {
  font-size: 30px;
  color: black;
}
button {
  margin-top: 20px;
  align-self: center;
  padding: 1em 2em;
  font-family: "Popins", sans-serif;
  font-size: 15px;
  background-color: black;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
</style>

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
// import { ethers } from "ethers";
export default {
  name: "App",
  components: {},
  data() {
    return {
      provider: undefined,
      fileList: undefined,
      fd: undefined,
    };
  },
  mounted() {
    document
      .getElementById("FILE")
      .addEventListener("change", async (event) => {
        this.fileList = event.target.files;
        this.fd = new FormData();
        this.fd.append("image", this.fileList[0]);
      });
  },
  async created() {
    //  this.provider = new ethers.providers.Web3Provider(window.ethereum)
    // await this.provider.send("eth_requestAccounts", []);
    // var dai = require("../../../artifacts/contracts/NFT.sol/MyNFT.json")
    // const daiContract = new ethers.Contract("0x5FbDB2315678afecb367f032d93F642f64180aa3", dai.abi, this.provider);
    // console.log(daiContract);
    // const signer = provider.getSigner()
  },
  methods: {
    async storeFiles(files) {
      const client = new Web3Storage("ejkkbwduewbewbcewbewbcewbccwe");
      const cid = await client.put(files);
      console.log("stored files with cid:", cid);
      return cid;
    },
    async showBlocks() {
      // var blocks = await this.provider.getBlockNumber()
    },
    buttonTrigger() {
      document.getElementById("FILE").click();
    },
  },
};
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

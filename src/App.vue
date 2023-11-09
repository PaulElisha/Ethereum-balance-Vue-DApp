<template>
  <div class="App">
    <nav>
      <h2>check your wallet balance</h2>
      <input
        placeholder="check address balance"
        v-model.trim="address"
        @keypress.enter="main"
      />
    </nav>
    <div v-if="showCard">
      <p>Your Balance is : {{ Balance }} (wei)</p>
    </div>
    <small>made with vue</small>
  </div>
</template>

<script setup>
import { ethers } from "ethers";
import { ref } from "vue";

const address = ref("");
const Balance = ref("");
const showCard = ref(false);

const main = async () => {
  const AlchemyApi =
    "https://eth-mainnet.g.alchemy.com/v2/4bYmhhbr7JU_nSwRzi6Wjaf08t4a22is";
  const provider = new ethers.JsonRpcProvider(AlchemyApi);

  Balance.value = await provider.getBalance(address.value);
  showCard.value = true;
  address.value = "";
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
nav {
  background-color: rgb(1, 1, 31);
  width: 100%;
  padding: 30px;
  display: flex;
  gap: 20px;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  box-shadow: 0px 10px 15px -3px rgba(0, 0, 0, 0.1);
}

nav h2 {
  font-size: 30px;
  font-weight: lighter;
  color: white;
}

nav input {
  padding: 15px;
  color: white;
  border: 2px solid white;
  border-radius: 4px;
}

p {
  margin: auto;
  margin-top: 30px;
  text-align: center;
  box-shadow: 0px 10px 15px -3px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  width: 420px;
  padding: 40px;
}
small {
  text-align: center;
  margin-top: 50px;
}
</style>

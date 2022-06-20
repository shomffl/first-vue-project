<script setup lang="ts">
import { ref, reactive, computed, watch, toRefs } from "vue";

const itemName1 = ref<string>("desk");
const itemName2 = "Bike";

const item1 = reactive({
  name: "Desk",
  price: 40000,
});

const price1 = 40000;
const price2 = 20000;

const url1 = "https://qiita.com/1060ki/items/1692f0e275634245c48d";

const buy = (itemName: String) => {
  alert("Are you sure to buy " + itemName + " ?");
};

const input = (e: any) => {
  item1.name = e.target.value;
};

const inputPrice = (e: any) => {
  item1.price = e.target.value;
};

const clear = () => {
  item1.name = "";
  item1.price = 0;
};

const budget = 50000;

const priceLabel = ref<string>(item1.price + "yen");
const { price } = toRefs(item1);
watch(price, () => {
  if (price.value > budget * 2) {
    priceLabel.value = "tooooo expensive";
  } else if (price.value > budget) {
    priceLabel.value = "expensive";
  } else {
    priceLabel.value = priceLabel.value + "yen";
  }
});
</script>

<template>
  <div class="container">
    <h1>最近の支出</h1>
    <input v-model="item1.name" />
    <input v-on:input="inputPrice" v-bind:value="item1.price" />
    <button v-on:click="clear">Clear</button>
    <div class="payment">
      <label>{{ item1.name }}</label>
      <label>{{ priceLabel }}</label>
      <a v-bind:href="url1">bought at ...</a>
      <button @click="buy(itemName1)">BUY</button>
    </div>
    <div class="payment">
      <label>{{ itemName2 }}</label> <label>{{ price2 }}</label>
      <button v-on:click="buy(itemName2)">BUY</button>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.payment {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 80px;
  width: 400px;
  background-color: aliceblue;
}

label {
  font-size: 20px;
  font-weight: bold;
}
</style>

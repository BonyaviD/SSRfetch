<template>
  <div v-if="status">
  <div>{{ status }}</div>
    <div class="cards" v-for="product in productsListData">
      <div class="card" v-for="card in product" :key="card.ProductId">
        <div>{{ card.Title }}</div>
        <div>{{ card.ProductPrice }}</div>
        <div>{{ card.BrandName }}</div>
        <img :src="`https://www.gholabcdn.com/${card.Image}`" :alt="card.Title">
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const payload = {
  DirectUrl: "",
  brandName: "",
  category1: "لپ-تاپ",
  category2: "",
  category3: "",
  filterItems: "",
  pageNumber: 1,
  pageSize: 40,
  searchText: "",
};

const productsListData = ref([])

const { data, status, error, refresh, clear } = await useAsyncData("mountains", () =>
  $fetch("https://pwa.gholab.ir/api/TotalData/ListPageTotalData", {
    method: "POST", // روش ارسال درخواست
    body: payload, // ارسال payload
    mode: "no-cors",
  })
);

productsListData.value.push(data.value.Data.Value.ProductList.PorductList)

</script>

<style scoped>
.cards {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 2rem;
  flex-wrap: wrap;
}
.card {
  background-color: gray;
  font-size: 1rem;
  width: 300px;
  height: 400px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

img {
  width: 200px;
  height: 200px;
  object-fit: cover;
}
</style>



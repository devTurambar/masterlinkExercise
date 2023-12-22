<script setup lang="ts">
  import { ref, defineProps, watchEffect } from 'vue';

  // Define cardData as a prop...need defineprops to access props on the script setup
  const props = defineProps(["cardData"]);

  //Use a ref to store the fetched data
  const fetchedData = ref({ value: null });

  // Use watchEffect to trigger the fetch when cardData changes
  watchEffect(async () => {
    if (props.cardData) {
      const link = props.cardData;
      await fetchData(link);
    }
  });

  // Function to fetch data
  async function fetchData(link) {
    try {
        const response = await useFetch(link);
        fetchedData.value = response.data.value; // Update fetchedData with the actual 
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  }
</script>

<template>
    <label :for="cardInfo"></label>
    <!--Check if fetchedData.value is not null -->
    <div v-if="fetchedData" class="cardsContainer">
        <input v-for="(item,index) in fetchedData.data" :key="index" type="image" :src="item.imageUri" :alt="item.text" :formaction="item.link" width="250" height="100" />
    </div>
</template>

<style scoped>
    .cardsContainer{
        display: flex;
        flex-direction: column;
        gap:20px;
        margin-top:50px;
        align-items: center;
    }
</style>

<script setup lang="ts">
  const { data: fetchedData } = await useFetch('https://masterlink-mock-api.mwe.pt/MlkApi/bpm_metadata/1');
</script>
<template>
  <div id="mainContainer">
    <DynamicForm :initialData="fetchedData" />
  </div>
</template>

<script lang="ts">
  //TODO Create fetch component to use here and re-use in the cards compoent
  export default {

  };
</script>
<style scoped>
  #mainContainer{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>

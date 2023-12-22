<template>
    <!-- TODO Make this component work, so I can re-use it...didn't had the time -->
    <div v-if="fetchedData">
    <!-- Render fetched data using a slot -->
    <slot :data="fetchedData.value">ds</slot>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  props: {
    url: {
      type: String,
      required: true,
    },
  },
  setup() {
    const fetchedData = ref(null);

    return {
      fetchedData,
    };
  },
  async fetch() {
    try {
      const response = await this.$fetch.get(this.url); // Assuming $fetch is available in Nuxt context
      this.fetchedData = response.data;
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  },
};
</script>

<style scoped>
</style>

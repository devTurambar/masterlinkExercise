<template>
<h2>{{ formData.formName }}</h2>
    <div>
    <form @submit.prevent="submitForm" :name="formData.formName" :id="formData.id" class="formContainer">
        <div class="nonCardsContainer">
        <div v-for="(item,index) in formData.nonCardsFields" :key="index" :fieldData="item" >
            <Field :fieldData="item" />
        </div>
        </div>
        <div v-for="(item,index) in formData.cardsFields" :key="index" :fieldData="item">
            <Card :cardData="item.dataUri" id="111"/>
        </div>
    </form>
    </div>
</template>

<script>
export default {
  props: ['initialData'], // Define props to receive data from the parent
  //state here
  data() {
    //TODO change this...
    //Should use for each when creating these 2 arrays instead of filter...so i don't run 2 times through the original array...
    //Separeted in two arrays here, before going to the template, so i can style the containers separetedly, nonCards and cards container
    const nonCardsArr = JSON.parse(JSON.stringify(this.initialData.fields.filter((e) =>  e.type !== "card"
    )));
    const cardsArr = JSON.parse(JSON.stringify(this.initialData.fields.filter((e) =>  e.type === "card"
    ))); 
    return {
        formData: {
            formName: this.initialData.title || "",
            nonCardsFields: nonCardsArr || "",
            cardsFields: cardsArr || "",
            id: this.initialData.id || "",
        },
    };
  },

  methods: {
    submitForm() {
      // Handle form submission logic here
      console.log('Form submitted:', this.formData);
    },
  },
};
</script>

<style scoped>
  .formContainer{
    display: flex;
    flex-direction: column;
  }
  .nonCardsContainer{
    display: flex;
    flex-direction: row;
    gap:20px;
  }
</style>

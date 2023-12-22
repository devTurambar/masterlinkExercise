<template>
    <label :for="fieldInfo.id">{{fieldInfo.name}}</label>
    <input :type="fieldInfo.type" :id="fieldInfo.id" required />       
</template>
<script>
    export default{
        props: ["fieldData"],
        data(){
            return{
                fieldInfo: {
                    id: this.fieldData.id || "",
                    type: this.fieldData.type || "",
                    name: this.fieldData.name || "",
                    dataUri: this.fieldData.dataUri || "",
                },
            }
        }
    }
</script>
<style scoped>
    label{
        margin-right:5px;
    }
</style>

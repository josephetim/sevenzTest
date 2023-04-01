<template>
    <div>
      <b-form-select :disabled=true v-model="selected" :placeholder="'pecify'" :options="optionsData"></b-form-select>    </div>
  </template>
  
  <script>
    export default {
      data() {
        const optionsArray = Array.isArray(this.options) ? this.options : [this.options];
        return {
          
          optionsData: [
      { value: null, text: '*Specify' },
            ...optionsArray
    ]
        }
      },
      props: ['optionsData']
    }
  </script>
<template>
    <div>
      <div v-for="imaging in imagingData" :key="imaging.id">
        <p class="avenir-normal-900 purple imaging-header">{{ imaging.title }}</p>
        <div id="xray-checkbox" class="d-flex flex-row flex-wrap align-items-around">
          <div class="form-check checkbox" v-for="investigation in imaging.investigations" :key="investigation.id">
            <input class="form-check-input" type="checkbox" :value="investigation.id" v-model="selectedItems" :id="investigation.id">
            <label class="form-check-label line-height-20" :for="investigation.id">{{ investigation.title }}</label>
          </div>
        </div>
        <hr />
      </div>
    </div>
  </template>


<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Lato');
.purple{
    color:  #382F90;
}
.imaging-header {
        font-size: 18px;
        line-height: 25px;
}
.avenir-normal-900 {
    font-family: "Avenir";
    font-style: normal;
    font-weight: 900;
}
.form-check-label {
  font-family: 'Lato';
}
.checkbox {
        width: 174px;
        font-family: 'Lato';

    }
    #xray-checkbox {
        gap:30px 35px;
    }
@media (max-width: 809px) {
    #xray-checkbox {
        gap: 10px 10px;
    }
    .checkbox {
        width: 100px;
    }
}
</style>

<script>
export default {
  data() {
    return {
      selectedItems: [],
    };
  },
  props: {
    imagingData: {
      type: Array,
      required: true,
    },
  },
  methods: {
    emitSelectedItems() {
      this.$emit("selected-items", this.selectedItems);
    },
  },
  watch: {
    selectedItems() {
      this.emitSelectedItems();
    },
  },
};
</script>
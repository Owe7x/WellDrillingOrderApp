<template>
  <div id="app">
    <div class="ui main container">
      <MyForm :form="form" @onFormSubmit="onFormSubmit" />
    </div>
  </div>
</template>

<script>

import MyForm from "@/components/MyForm";


export default {
  name: "App",
  components: {
    MyForm,
  },
  data() {
    return {
      form: { customer: "", 
              contractor: "", 
              oilField: "", 
              wellNumber: "", 
              wellPurpose: "", 
              drillingRig: "", 
              wellDesign: "",
              direction: "", 
              conductor: "", 
              operatingColumn: "", 
              diameter: "", 
              artificialFaceDepth: "", 
              oilFinstallationDepthield: "", 
              isEdit: false 
            },
    };
  },
  methods: {
    onFormSubmit(data) {
      // window.console.log("app onFormSubmit", data);

      if (data.isEdit) {
        // call edit customer
        this.editCustomer(data);
      } else {
        // call create customer
        this.createCustomer(data);
      }
    }
  },
};
</script>

<style>
.vue-color {
  background: #41b883 !important;
}

.main.container {
  margin-top: 60px;
}

.submit-button {
  margin-top: 24px !important;
  float: right;
}

.data {
  margin-top: 15px;
}

thead tr th {
  background: #e0e0e0 !important;
}

.ui.inverted.dimmer {
  background-color: rgba(255, 255, 255, 0) !important;
}
</style>

<template>
  <div id="app">
    <div class="ui main container">
      <Loader v-if="loader" />
      <CustomerList
        :customers="customers"
        @onDelete="onDelete"
        @onEdit="onEdit"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CustomerList from "@/components/CustomerList";
import Loader from "@/components/Loader";

export default {
  name: "App",
  components: {
    CustomerList,
    Loader
  },
  data() {
    return {
      url: "http://laravel.loc/api/customers",
      customers: [],
      loader: false
    };
  },
  methods: {
    getCustomers() {
      this.loader = false;

      axios.get(this.url).then(data => {
        this.customers = data.data;
        this.loader = false;
      });
    },
    deleteCustomer(id) {
      this.loader = true;

      axios
        .delete(`${this.url}/${id}`)
        .then(() => {
          this.getCustomers();
        })
        .catch(e => {
          alert(e);
        });
    },
    createCustomer(data) {
      this.loader = true;

      axios
        .post(this.url, {
          customer: data.customer,
          contractor: data.contractor,
          oilField: data.oilField,
          wellNumber: data.wellNumber,
          wellPurpose: data.wellPurpose,
          drillingRig: data.drillingRig,
          wellDesign: data.wellDesign,
          direction: data.direction,
          conductor: data.conductor,
          operatingColumn: data.operatingColumn,
          diameter: data.diameter,
          artificialFaceDepth: data.artificialFaceDepth,
          installationDepth: data.installationDepth,
        })
        .then(() => {
          this.getCustomers();
        })
        .catch(e => {
          alert(e);
        });
    },
    editCustomer(data) {
      this.loader = true;

      axios
        .put(`${this.url}/${data.id}`, {
          customer: data.customer,
          contractor: data.contractor,
          oilField: data.oilField,
          wellNumber: data.wellNumber,
          wellPurpose: data.wellPurpose,
          drillingRig: data.drillingRig,
          wellDesign: data.wellDesign,
          direction: data.direction,
          conductor: data.conductor,
          operatingColumn: data.operatingColumn,
          diameter: data.diameter,
          artificialFaceDepth: data.artificialFaceDepth,
          installationDepth: data.installationDepth,
        })
        .then(() => {
          this.getCustomers();
        })
        .catch(e => {
          alert(e);
        });
    },
    onDelete(id) {
      // window.console.log("app delete " + id);

      this.deleteCustomer(id);
    },
    onEdit(data) {
      // window.console.log("app edit ", data);

      this.form = data;
      this.form.isEdit = true;
    },
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
  created() {
    this.getCustomers();
  }
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

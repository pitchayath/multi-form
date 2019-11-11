<template>
  <div>
    <h1>Multiple Customer Information Recording</h1>
    <el-button @click="addNewForm">Add Customer</el-button>
    <el-button type="primary" @click="submit" :disabled="this.customers.length === 0">Save</el-button>
    <hr/>
    <customer-form v-for="(customer, index) in customers" :key="customer.id" :id="customer.id" v-model="customers[index]" :validation="validations[index]" />
    <el-dialog title="Confirm" :visible.sync="confirm" :before-close="handleClose" width="30%">
      <span>{{ customersData }}</span>
      <span slot="footer" class="dialog-footer">
        <el-button type="primary" @click="handleClose">Close</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
import CustomerForm from './CustomerForm';

export default {
  name: 'multi-form',
  components: {
    CustomerForm,
  },
  data() {
    return {
      runningId: 1,
      customers: [],
      validations: [],
      customersData: '',
      confirm: false,
    };
  },
  methods: {
    addNewForm() {
      this.customers.push({ id: this.runningId++, name: '', email: '', juices: ''});
      this.validations.push({ name: { valid: true }, email: { valid: true }, juices: { valid: true }});
    },
    validate() {
      for (let i = 0; i < this.customers.length; i++) {
        const customer = this.customers[i];
        const validation = this.validations[i];

        validation.name.valid = customer.name.length > 0;
        validation.email.valid = customer.email.length > 0;
        validation.juices.valid = customer.juices.length > 0;
      }

      return this.validations.every(v => this.customerValid(v));
    },
    customerValid(validation) {
      return validation.name.valid && validation.email.valid && validation.juices.valid;
    },
    submit() {
      const valid = this.validate();
      if (valid) {
        this.customersData = JSON.stringify(this.customers);
        this.confirm = true;
      }
    },
    handleClose() {
      this.confirm = false;
      this.reset();
    },
    reset() {
      this.runningId = 1;
      this.customers = [];
      this.validations = [];
      this.customersData = '';
    }
  },
}
</script>

<style>

</style>
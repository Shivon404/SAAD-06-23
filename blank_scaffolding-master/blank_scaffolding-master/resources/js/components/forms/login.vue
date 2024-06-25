<template>
  <div>
    <bootstrap-form @submit="submitForm"></bootstrap-form>
    <b-table striped hover :items="items" :fields="fields"></b-table>
  </div>
</template>

<script>
import BootstrapForm from './bootstrap-form.vue'; 
import axios from 'axios'; 

export default {
  components: {
    BootstrapForm
  },
  data() {
    return {
      items: null,
      fields: ['id', 'USERNAME']
    }
  },
  methods: {
    get_accounts() {
      axios.get('/get_accounts')
        .then(response => {
          console.log(response.data);
          this.items = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    },
    submitForm(formData) {
      axios.post('/login', formData)
        .then(response => {
          console.log(response.data);
          // Handle success response
        })
        .catch(error => {
          console.error(error);
          // Handle error response
        });
    }
  },
  beforeMount() {
    this.get_accounts();
  }
}
</script>

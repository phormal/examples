<template>
  <div id="phormal"></div>
</template>

<script>
import {Phormal, useLength, useEmail, useRequired} from '@phormal/core';

export default {
  name: 'PhormalContent',

  data() {
    return {
      formFields: {
        paymentMethod: {
          type: 'radiogroup',
          label: 'Payment Method',
          value: 'paypal',
          options: [
            {label: 'PayPal', value: 'paypal'},
            {label: 'Credit card', value: 'creditcard'},
            {label: 'Klarna', value: 'klarna'},
          ]
        },
        name: {
          label: 'Name',
          hooks: [useRequired(), useLength(3)]
        },
        email: {
          label: 'Email',
          hooks: [useRequired(), useEmail()]
        },
        newsletter: {
          type: 'checkbox',
          label: 'Newsletter',
          value: true
        },
      },
      formConfig: {
        theme: 'basic',
        el: '#phormal',
        language: 'en'
      },
      form: null
    }
  },

  mounted() {
    this.form = new Phormal(this.formFields, this.formConfig);
  },

  methods: {
    validate() {
      this.form.$validate();
    },

    getValues() {
      return this.form.$values(); // { name: 'John Doe' }
    }
  },

  watch: {
    'form.name': {
      handler: function (val) {
        console.log('name changed to', val);
      },
    }
  }
};
</script>

<style>
@import '@phormal/theme-basic/dist/index.css';

#phormal {
  font-family: sans-serif;
}
</style>

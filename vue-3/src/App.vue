<script setup>
import {ref, onMounted} from "vue";
import {Phormal, useLength, useEmail, useRequired} from "@phormal/core";

const formFields = {
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
  deliveryMethod: {
    type: 'radiogroup',
    options: [
      {label: 'PayPal', value: 'paypal'},
      {label: 'Credit card', value: 'creditcard'},
      {label: 'Klarna', value: 'klarna'},
    ]
  }
}

const formConfig = {
  theme: 'basic',
  el: '#phormal',
  language: 'en'
}

const phormal = ref(null);

onMounted(() => {
  phormal.value = new Phormal(formFields, formConfig);
});

</script>

<template>
  <div>
    <div id="phormal"></div>
  </div>
</template>

<style>
@import '@phormal/theme-basic/dist/index.css';

#phormal {
  margin: 0 auto;
  width: 100%;
  max-width: 600px;
}
</style>

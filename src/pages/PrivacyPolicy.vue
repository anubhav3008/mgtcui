<template>
  <main-layout>
    <privacy-policy-component></privacy-policy-component>
  </main-layout>
</template>

<script>
  import MainLayout from '../layouts/Main.vue'
  import PrivacyPolicyComponent from '../components/PrivacyPolicyComponent.vue'
  export default {
    components: {
      MainLayout,
        PrivacyPolicyComponent
    }
  }
</script>

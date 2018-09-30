<template>
  <main-layout>
    <contribution-component></contribution-component>
  </main-layout>
</template>

<script>
  import MainLayout from '../layouts/Main.vue'
  import ContributionComponent from '../components/ContributionComponent.vue'
  export default {
    components: {
      MainLayout,
        ContributionComponent
    }
  }
</script>

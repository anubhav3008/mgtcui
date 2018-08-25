<template>
  <main-layout>
    <add-meeting-component></add-meeting-component>
    <listing-component></listing-component>

  </main-layout>
</template>

<script>
  import MainLayout from '../layouts/Main.vue'
  import ListingComponent from '../components/ListingComponent.vue'
  import AddMeetingComponent from '../components/AddMeetingComponent.vue'
  export default {
    components: {
      MainLayout,
        ListingComponent,
        AddMeetingComponent
    }
  }
</script>

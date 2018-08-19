<template>
  <main-layout>
     <listing-component></listing-component>
     <meeting-details-component></meeting-details-component>
    <add-meeting-component></add-meeting-component>
  </main-layout>
</template>

<script>
  import MainLayout from '../layouts/Main.vue'
  import ListingComponent from '../components/ListingComponent.vue'
  import MeetingDetailsComponent from '../components/MeetingDetailsComponent.vue'
  import AddMeetingComponent from '../components/AddMeetingComponent.vue'
  export default {
    components: {
      MainLayout,
        ListingComponent,
        MeetingDetailsComponent,
        AddMeetingComponent
    }
  }
</script>

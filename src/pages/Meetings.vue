<template>
  <main-layout>
    <add-meeting-component></add-meeting-component>
  </main-layout>
</template>

<script>
  import MainLayout from '../layouts/Main.vue'
  import AddMeetingComponent from '../components/AddMeetingComponent.vue'
  export default {
    components: {
      MainLayout,
        AddMeetingComponent
    }
  }
</script>

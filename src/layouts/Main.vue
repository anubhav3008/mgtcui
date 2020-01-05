<template>
<div>
  <b-nav pills tabs>
      <b-nav-item><v-link href="/meetings">Meeting</v-link></b-nav-item>
      <b-nav-item><v-link href="/search">Search</v-link></b-nav-item>
      <b-nav-item><v-link href="/contribution">Contribution</v-link></b-nav-item>
      <b-nav-item><v-link href="/leaderBoard">LeaderBoard</v-link></b-nav-item>
      <b-nav-item><v-link href="/privacy">PrivacyPolicy</v-link></b-nav-item>
  </b-nav>
  <slot></slot>
</div>
</template>

<script>
  import VLink from '../components/VLink.vue'
  export default {
    components: {
      VLink
    }
  }
</script>
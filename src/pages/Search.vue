<template>
    <main-layout>
        <listing-component></listing-component>
    </main-layout>
</template>

<script>
    import MainLayout from '../layouts/Main.vue'
    import ListingComponent from '../components/ListingComponent.vue'
    export default {
        components: {
            MainLayout,
            ListingComponent,
        }
    }
</script>

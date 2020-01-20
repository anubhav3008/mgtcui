<template>
    <main-layout>
        <users-component></users-component>
    </main-layout>
</template>

<script>
    import MainLayout from '../layouts/Main.vue'
    import UsersComponent from '../components/UsersComponent.vue'
    export default {
        components: {
            MainLayout,
            UsersComponent
        }
    }
</script>

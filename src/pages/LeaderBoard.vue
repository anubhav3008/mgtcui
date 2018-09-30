<template>
    <main-layout>
        <leader-board-component></leader-board-component>
    </main-layout>
</template>

<script>
    import MainLayout from '../layouts/Main.vue'
    import LeaderBoardComponent from '../components/LeaderBoardComponent.vue'
    export default {
        components: {
            MainLayout,
            LeaderBoardComponent
        }
    }
</script>

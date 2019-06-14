<template>
    <div>
    <b-table striped hover small responsive=true stacked="md" :items="stats.data"></b-table>
    </div>
</template>

<script>

    import axios from 'axios'
    import VueAxios from 'vue-axios'
    import Vue from 'vue'
    Vue.use(VueAxios, axios)
    export default {

        data(){
            return{
                stats:"",
              }
        },
        methods: {
            search(){
                axios
                    .get('https://sarjapura-toastmasters-api.herokuapp.com/leaderboard/byName')
                    .then(response => (this.stats = response.data))
                    .catch(error => console.log(error))
            }
        },
        created:function () {
         this.search();
        }
    }
</script>
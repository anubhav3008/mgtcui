<template>
    <div>
    <b-table striped hover small responsive=true stacked="md" :items="meetingList.data"></b-table>
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
                meetingList:"",
              }
        },
        methods: {
            search(){
                axios
                    .get('https://mgtc.herokuapp.com/meetings')
                    .then(response => (this.meetingList = response.data))
                    .catch(error => console.log(error))
            }
        },
        created:function () {
         this.search();
        }
    }
</script>
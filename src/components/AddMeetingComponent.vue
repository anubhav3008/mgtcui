<template>
    <div>
     <button  v-on:click="search">Add Meetings</button>
        {{meetingList}}
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
                    .get('http://mgtc.herokuapp.com/meetings/')
                    .then(response => (this.meetingList = response.data))
                    .catch(error => console.log(error))
            }

        }
    }
</script>
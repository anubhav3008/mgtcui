<template>
    <div>
     <button  v-on:click="search">All Meetings</button>


        <table class="table table-condensed" v-if="meetingList.data">
            <thead>
            <tr>
                <th>id</th>
                <th>TTM</th>
                <th>Grammarian</th>
                <th>Ah counter</th>
                <th>TMOD</th>
                <th>Timer</th>
                <th>GE</th>
                <th>Theme</th>
            </tr>
            </thead>
            <tbody>
            <tr  v-for="meeting in meetingList.data" :key="meeting.id">
                <td>{{meeting.id}}</td>
                <td>{{meeting.ttmName}}</td>
                <td>{{meeting.grammarianName}}</td>
                <td>{{meeting.ahCounterName}}</td>
                <td>{{meeting.tmodName}}</td>
                <td>{{meeting.timerName}}</td>
                <td>{{meeting.geName}}</td>
                <td>{{meeting.theme}}</td>
            </tr>
            </tbody>
        </table>

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
                    .get('https://mgtc.herokuapp.com/meetings/')
                    .then(response => (this.meetingList = response.data))
                    .catch(error => console.log(error))
            }

        }
    }
</script>
<template>
    <div>
    <input type="text" v-model="meetingNumber"/>
    <button  v-on:click="search">Search Meeting</button>

        
        <table class="table table-condensed" v-if="meetingDetails.data && meetingDetails.data.meeting">
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
            <tr>
                <td>{{meetingDetails.data.meeting.id}}</td>
                <td>{{meetingDetails.data.meeting.ttmName}}</td>
                <td>{{meetingDetails.data.meeting.grammarianName}}</td>
                <td>{{meetingDetails.data.meeting.ahCounterName}}</td>
                <td>{{meetingDetails.data.meeting.tmodName}}</td>
                <td>{{meetingDetails.data.meeting.timerName}}</td>
                <td>{{meetingDetails.data.meeting.geName}}</td>
                <td>{{meetingDetails.data.meeting.theme}}</td>
            </tr>
            </tbody>
        </table>



        <table class="table table-condensed" v-if="meetingDetails.data && meetingDetails.data.speech">
            <thead>
            <tr>
                <th>id</th>
                <th>project</th>
                <th>Speaker Name</th>
                <th>Speaker ID</th>
                <th>Evaluator Name</th>
                <th>Evaluator id</th>
                <th>date</th>
                <th>Time min</th>
                <th>Time max</th>
            </tr>
            </thead>
            <tbody>
            <tr  v-for="meeting in meetingDetails.data.speech" :key="meeting.id">
                <td>{{meeting.id}}</td>
                <td>{{meeting.projectName}}</td>
                <td>{{meeting.speakerName}}</td>
                <td>{{meeting.speakerId}}</td>
                <td>{{meeting.evaluatorName}}</td>
                <td>{{meeting.evaluatorId}}</td>
                <td>{{meeting.date}}</td>
                <td>{{meeting.timeMin}}</td>
                <td>{{meeting.timeMax}}</td>
            </tr>
            </tbody>
        </table>


         <table class="table table-condensed" v-if="meetingDetails.data && meetingDetails.data.goal">
            <thead>
            <tr>
                <th>id</th>
                <th>user Id</th>
                <th>user name</th>
                <th>Project Name</th>
                <th>date</th>
                <th>meeting Id</th>
            </tr>
            </thead>
            <tbody>
            <tr  v-for="goal in meetingDetails.data.goal" :key="goal.id">
                <td>{{goal.id}}</td>
                <td>{{goal.userId}}</td>
                <td>{{goal.userName}}</td>
                <td>{{goal.projectName}}</td>
                <td>{{goal.date}}</td>
                <td>{{goal.meetingId}}</td>
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
                meetingDetails:"",
                meetingNumber:""
            }
        },
        methods: {
            search(){
                axios
                    .get('https://mgtc.herokuapp.com/meetings/'+this.meetingNumber)
                    .then(response => (this.meetingDetails = response.data))
                    .catch(error => console.log(error))
            }

        }
    }
</script>
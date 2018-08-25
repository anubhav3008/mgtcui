<template>
    <div>
        Meeting summary:
        <table class="table table-condensed">
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
                <td><input type="text" v-model="meeting.id"/></td>
                <td><input type="text" v-model="meeting.ttmName"/></td>
                <td><input type="text" v-model="meeting.grammarianName"/></td>
                <td><input type="text" v-model="meeting.ahCounterName"/></td>
                <td><input type="text" v-model="meeting.tmodName"/></td>
                <td><input type="text" v-model="meeting.timerName"/></td>
                <td><input type="text" v-model="meeting.geName"/></td>
                <td><input type="text" v-model="meeting.theme"/></td>
            </tr>
            </tbody>
        </table>
        Speech
        <input type="text" v-model="speech_project"/>
        <input type="text" v-model="speech_speaker_name"/>
        <input type="text" v-model="speech_speaker_id"/>
        <input type="text" v-model="speech_evaluator_name"/>
        <input type="text" v-model="speech_evaluator_id"/>
        <input type="text" v-model="speech_date"/>
        <input type="text" v-model="speech_time_min"/>
        <input type="text" v-model="speech_time_max"/>
        <button v-on:click="addSpeech">Add speech</button>
        <table class="table table-condensed" v-if="speech">
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
            <tr  v-for="meeting in speech" :key="meeting.id">
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

        Goals
        <input type="text" v-model="goal_userId"/>
        <input type="text" v-model="goal_userName"/>
        <input type="text" v-model="goal_projectName"/>
        <input type="text" v-model="goal_date"/>
        <input type="text" v-model="goal_meeting_id"/>
        <button v-on:click="addGoal">Add Goal</button>
        <table class="table table-condensed" v-if="goal">
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
            <tr  v-for="goal in goal" :key="goal.id">
                <td>{{goal.id}}</td>
                <td>{{goal.userId}}</td>
                <td>{{goal.userName}}</td>
                <td>{{goal.projectName}}</td>
                <td>{{goal.date}}</td>
                <td>{{goal.meetingId}}</td>
            </tr>
            </tbody>
        </table>

        <button  v-on:click="addOrUpdate">Add/update Meeting</button>
        <input type="text" v-model="searchMeetingNumber"/>
        <button  v-on:click="search">Search Meeting</button>

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
                meeting:{},
                goal:[],
                speech:[],
                speech_project:"",
                speech_speaker_name:"",
                speech_speaker_id:"",
                speech_evaluator_name:"",
                speech_evaluator_id:"",
                speech_date:"",
                speech_time_min:"",
                speech_time_max:"",
                goal_userId:"",
                goal_userName:"",
                goal_projectName:"",
                goal_date:"",
                goal_meeting_id:"",
                searchMeetingNumber:""
              }
        },

        methods: {
            addOrUpdate(){
                axios
                    .post('https://mgtc.herokuapp.com/meetings/addOrUpdate',
                        {
                            meeting:  this.meeting,
                            goal:this.goal,
                            speech:this.speech
                        }
                    )
                    .then(response => (this.meetingList = response.data))
                    .catch(error => console.log(error))
            },
            addSpeech(){
                this.speech.push({
                    projectName : this.speech_project,
                    speakerName: this.speech_speaker_name,
                    speakerId : this.speech_speaker_id,
                    evaluatorName:this.speech_evaluator_name,
                    evaluatorId:this.speech_evaluator_id,
                    date: this.speech_date,
                    timeMin:this.speech_time_min,
                    timeMax:this.speech_time_max
                })
        },
            addGoal(){
                this.goal.push({
                    userId:this.goal_userId,
                    userName:this.goal_userName,
                    projectName: this.goal_projectName,
                    date:this.goal_date,
                    meetingId:this.goal_meeting_id
                })
            },
            search(){
                axios
                    .get('https://mgtc.herokuapp.com/meetings/'+this.searchMeetingNumber)
                    .then((response) => {
                        this.goal = response.data.data.goal;
                        this.speech=response.data.data.speech;
                        this.meeting=response.data.data.meeting;
                    })
                    .catch(error => console.log(error))
            }
        }
    }
</script>
<template>
    <div>
    <div align="right">
    <b-form inline>
    <b-form-input type="text" placeholder="meeting number" v-model="searchMeetingNumber"/>
    <b-button variant="primary" v-on:click="search">Fetch meeting</b-button>
    </b-form>
    </div>
    <b-form inline>
                <b-col lg="2">Meeting number</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.id" placeholder="meeting number"> </b-form-input></b-col> 
                <b-col lg="2">TTM name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.ttmName"  placeholder="ttm name"/> </b-form-input></b-col> 
                <b-col lg="2">Grammarian name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.grammarianName"  placeholder="grammarian name"/> </b-form-input></b-col> 
                <b-col lg="2">Ah counter name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.ahCounterName"  placeholder="ah counter name"/> </b-form-input></b-col> 
                <b-col lg="2">TMOD name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.tmodName"  placeholder="tmod name"/> </b-form-input></b-col> 
                <b-col lg="2">Timer name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.timerName" placeholder="timer name"/> </b-form-input></b-col> 
                <b-col lg="2">GE name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.geName" placeholder="GE name"/> </b-form-input></b-col> 
                <b-col lg="2">Theme</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.theme"  placeholder="theme"/> </b-form-input></b-col> 
    </b-form>

    <br>
    <hr>
    <b-form inline>
            
            <b-col lg="3"><b-form-input type="text" v-model="speech_project" placeholder="speech project name"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_speaker_name" placeholder="speech speaker name"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_speaker_id" placeholder="speech speaker id"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_evaluator_name" placeholder="speech evaluator name"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_evaluator_id" placeholder="speech evaluator id"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="date" v-model="speech_date" placeholder="speech date"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_time_min" placeholder="min time"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_time_max" placeholder="max time"></b-form-input></b-col> 
    </b-form>
    <div align="center">
            <b-button variant="primary" v-on:click="addSpeech">Add speech</b-button>
    </div>
    <hr>
    <b-table striped hover small responsive=true stacked="md" :items="speech"></b-table>
    <b-form inline>
        <b-col lg="4"><b-form-input type="text" v-model="goal_userId" placeholder="user id"/></b-col>
        <b-col lg="4"><b-form-input type="text" v-model="goal_userName" placeholder="user name"/></b-col>
        <b-col lg="4"><b-form-input type="text" v-model="goal_projectName" placeholder="project name"/></b-col>
        <b-col lg="4"><b-form-input type="text" v-model="goal_date" placeholder="date"/></b-col>
        <b-col lg="4"><b-form-input type="text" v-model="goal_meeting_id" placeholder="meeting number"/></b-col>
    </b-form>
     <div align="center">
         <b-button variant="primary" v-on:click="addGoal">Add Goal</b-button>
    </div>
    <b-table striped hover small responsive=true stacked="md" :items="goal"></b-table>
     <div align="center">
         <b-button variant="primary" v-on:click="addOrUpdate">Add/update Meeting</b-button>
    </div>
    </div>
</template>

<script>

    import axios from 'axios'
    import VueAxios from 'vue-axios'
    import Vue from 'vue'
    import BootstrapVue from 'bootstrap-vue'
    import 'bootstrap/dist/css/bootstrap.css'
    import 'bootstrap-vue/dist/bootstrap-vue.css'
    Vue.use(VueAxios, axios);
    Vue.use(BootstrapVue);

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
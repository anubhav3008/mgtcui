<template>
    <div>
          <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">


    <div align="right">
    <b-form inline>
    <b-form-input type="text" placeholder="meeting number" v-model="searchMeetingNumber"/>
    <b-button variant="primary" v-on:click="search">Fetch meeting</b-button>
    </b-form>
    </div>

    <b-form inline>
    <datalist id="usersDiv">
        <option v-for="user in users" v-bind:value="user.name"  v-bind:label="user.name">
        </option>
    </datalist>

    <datalist id="autosuggestionDiv">
        <option v-for="auto in autosuggestion" v-bind:value="auto"  v-bind:label="auto">
        </option>
    </datalist>
                <b-col lg="2">Meeting number</b-col>
                <b-col lg="10"><b-form-input type="text" v-model="meeting.id" placeholder="meeting number"> </b-form-input></b-col> 
                <b-col lg="2">TTM name</b-col>
                <b-col lg="10">
                <b-form-input type="text" v-model="meeting.ttmName" placeholder="ttm name" list="usersDiv" v-on:change="getUsers">
                </b-form-input>
                </b-col> 
                <b-col lg="2">TTM summary</b-col>
                <b-col lg="10">
                <vue-editor v-model="meeting.ttmSummary">
                </vue-editor>
                </b-col> 
                <b-col lg="2">Grammarian name</b-col>
                <b-col lg="10"><b-form-input type="text" v-model="meeting.grammarianName"  placeholder="grammarian name" list="usersDiv" v-on:change="getUsers"> </b-form-input></b-col>
                <b-col lg="2">Grammarian summary</b-col>
                <b-col lg="10">
                <vue-editor v-model="meeting.grammarianSummary">
                </vue-editor>
                </b-col> 
                <b-col lg="2">Ah counter name</b-col>
                <b-col lg="10"><b-form-input type="text" v-model="meeting.ahCounterName"  placeholder="ah counter name" list="usersDiv" v-on:change="getUsers"> </b-form-input></b-col>
                <b-col lg="2">Ah counter summary</b-col>
                <b-col lg="10">
                <vue-editor v-model="meeting.ahCounterSummary">
                </vue-editor>
                </b-col> 
                <b-col lg="2">TMOD name</b-col>
                <b-col lg="10"><b-form-input type="text" v-model="meeting.tmodName"  placeholder="tmod name" list="usersDiv" v-on:change="getUsers"> </b-form-input></b-col>
                <b-col lg="2">TMOD summary</b-col>
                <b-col lg="10">
                <vue-editor v-model="meeting.tmodSummary">
                </vue-editor>
                </b-col> 
                <b-col lg="2">Timer name</b-col>
                <b-col lg="10"><b-form-input type="text" v-model="meeting.timerName" placeholder="timer name" list="usersDiv" v-on:change="getUsers"> </b-form-input></b-col>
                <b-col lg="2">Timer summary</b-col>
                <b-col lg="10">
                <vue-editor v-model="meeting.timerSummary">
                </vue-editor>
                </b-col> 
                <b-col lg="2">GE name</b-col>
                <b-col lg="10"><b-form-input type="text" v-model="meeting.geName" placeholder="GE name" list="usersDiv"  v-on:change="getUsers"> </b-form-input></b-col>
                <b-col lg="2">GE summary</b-col>
                <b-col lg="10">
                <vue-editor v-model="meeting.geSummary">
                </vue-editor>
                </b-col> 
                <b-col lg="2">Theme</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.theme"  placeholder="theme"> </b-form-input></b-col>
                <b-col lg="2">Date</b-col>
                <b-col lg="4"><b-form-input type="date" v-model="meeting.date"  placeholder="date"> </b-form-input></b-col>
                 <b-col lg="2">Time</b-col>
                <b-col lg="4"><b-form-input type="time" v-model="meeting.time"  placeholder="time"> </b-form-input></b-col>
                <b-col lg="2">Club name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.clubName" placeholder="Club name" list="autosuggestionDiv"  v-on:change="getAutosuggestion"> </b-form-input></b-col>
                <b-col lg="2">Venue</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.venue" placeholder="Venue" list="autosuggestionDiv"  v-on:change="getAutosuggestion"> </b-form-input></b-col>
    </b-form>

    <br>
    <hr>
    <b-form inline>
            <b-col lg="3"><b-form-input type="text" v-model="speech_speaker_name" placeholder="speaker name" list="usersDiv" v-on:change="getUsers"></b-form-input></b-col> 
            <b-col lg="9">
                <vue-editor v-model="speech_speaker_summary">
                </vue-editor>
            </b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_evaluator_name" placeholder="evaluator name" list="usersDiv" v-on:change="getUsers"></b-form-input></b-col>
            <b-col lg="9">
                <vue-editor v-model="speech_evaluation_summary">
                </vue-editor>
            </b-col> 
    </b-form>
    <div align="center">
            <b-button variant="primary" v-on:click="addSpeech">Add speech</b-button>
    </div>
    
     <v-client-table :columns="speechTableFeilds" v-model="speech" :options="options">
    <div slot="name" slot-scope="{row, update, setEditing, isEditing, revertValue}">
      <span @click="setEditing(true)" v-if="!isEditing()">
        <a>{{row.name}}</a>
      </span>
      <span v-else>
        <input type="text" v-model="row.name">
        <button type="button" class="btn btn-info btn-xs" @click="update(row.name); setEditing(false)">Submit</button>
       <button type="button" class="btn btn-default btn-xs" @click="revertValue(); setEditing(false)">Cancel</button>
      </span>
   </div>
  </v-client-table>

    <b-table striped hover small responsive=true stacked="md" :items="speech" :fields="speechTableFeilds">

        <template slot="delete" slot-scope="row">
            <b-button size="sm" @click.stop="deleteSpeech(row.index)">Delete</b-button>

        </template>

    </b-table>
    
    <br>
     <div align="center">
         <b-button variant="primary" v-on:click="addOrUpdate">Add/update Meeting</b-button>
    </div>

    <hr>
    <div v-if= "meeting.ttmName || meeting.grammarianName || meeting.ahCounterName || meeting.tmodName || meeting.timerName || meeting.geName || meeting.theme || speech.length>0 || goal.length>0">
    
    <div align="center">
         <b-button variant="primary" v-on:click="save">Save</b-button>
         
    </div>
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
    import { VueEditor } from "vue2-editor"
    import Vuetify from 'vuetify/lib'
    import {ServerTable, ClientTable, Event} from 'vue-tables-2';
    Vue.use(ClientTable);
    Vue.use(VueAxios, axios);
    Vue.use(BootstrapVue);
    Vue.use(Vuetify)
    export default {

        data(){
            return{
                meeting:{},
                goal:[],
                speech:[],
                speech_project:"",
                speech_speaker_name:"",
                speech_evaluation_summary:"",
                speech_speaker_summary:"",
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
                searchMeetingNumber:"",
                speechTableFeilds:['id','speakerName', 'speech_speaker_summary','evaluatorName','speech_evaluation_summary','date','delete'],
                goalTableFeilds:['id','userId','userName','projectName','date','meetingId','delete'],
                users:[],
                userFetched:false,
                autosuggestion:[],
                autosuggestionFetched:false,
                options: {
                        headings: {
                                id: 'Id',
                                speakerName: 'Speaker name',
                                speech_speaker_summary: 'Speech summary',
                                evaluatorName: 'Evaluator Name',
                                speech_evaluation_summary: 'Evaluation Summary',
                                date: 'Date',
                                delete: 'Delete'
                                },
                        editableColumns:['speakerName','speech_speaker_summary','evaluatorName','speech_evaluation_summary','date'],
                        sortable: ['speakerName'],
                        filterable: ['speakerName']
                        }
              }
        },
        created:function () {
        this.getAutosuggestion();
         this.getUsers();
        },
        components: {
            VueEditor
        },
        methods: {
        getAutosuggestion(){
            if(this.autosuggestionFetched){
            return;
            }
            axios.get('https://sarjapura-toastmasters-api.herokuapp.com/autosuggest/static')
              .then(response => {
                this.autosuggestion = response.data.data;
                this.autosuggestionFetched=true;
              })
            },
            getUsers(){
              if(this.userFetched){
               return;
              }
              axios.get('https://sarjapura-toastmasters-api.herokuapp.com/users')
              .then(response => {
                this.users = response.data.data;
                this.userFetched=true;
              })
            },
            addOrUpdate(){
                axios
                    .post('https://sarjapura-toastmasters-api.herokuapp.com/meetings/addOrUpdate',
                        {
                            meeting:  this.meeting,
                            goal:this.goal,
                            speech:this.speech
                        }
                    )
                    .then(response => (alert(response.data.success)))
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
                    .get('https://sarjapura-toastmasters-api.herokuapp.com/meetings/'+this.searchMeetingNumber)
                    .then((response) => {
                        this.goal = response.data.data.goal;
                        this.speech=response.data.data.speech;
                        this.meeting=response.data.data.meeting;
                        alert("data fetched");
                    })
                    .catch(error => console.log(error))
            },
            deleteSpeech(index){
                this.speech.splice(index,1);
               },
            deleteGoal(index){
                this.goal.splice(index,1);
            } ,
            save(){
                if(this.meeting.id !=null){
                    window.location.href = 'http://sarjapura-toastmasters-api.herokuapp.com/communication/agenda/' + this.meeting.id;
                }
                else if(this.searchMeetingNumber !=null) {
                    window.location.href = 'http://sarjapura-toastmasters-api.herokuapp.com/communication/agenda/' + this.searchMeetingNumber;
                }
                else {
                    alert("Meeting id not found, please refresh and try again!")
                }
            }
        }
    }
</script>
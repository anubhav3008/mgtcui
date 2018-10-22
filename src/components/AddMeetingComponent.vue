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
                <b-col lg="4"><b-form-input type="text" v-model="meeting.id" placeholder="meeting number"> </b-form-input></b-col> 
                <b-col lg="2">TTM name</b-col>
                <b-col lg="4">
                <b-form-input type="text" v-model="meeting.ttmName" placeholder="ttm name" list="usersDiv" v-on:change="getUsers"/> 
                </b-form-input>
                </b-col> 
                <b-col lg="2">Grammarian name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.grammarianName"  placeholder="grammarian name" list="usersDiv" v-on:change="getUsers"/> </b-form-input></b-col> 
                <b-col lg="2">Ah counter name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.ahCounterName"  placeholder="ah counter name" list="usersDiv" v-on:change="getUsers"/> </b-form-input></b-col> 
                <b-col lg="2">TMOD name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.tmodName"  placeholder="tmod name" list="usersDiv" v-on:change="getUsers"/> </b-form-input></b-col> 
                <b-col lg="2">Timer name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.timerName" placeholder="timer name" list="usersDiv" v-on:change="getUsers"/> </b-form-input></b-col> 
                
                <b-col lg="2">GE name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.geName" placeholder="GE name" list="usersDiv"  v-on:change="getUsers"/> </b-form-input></b-col> 
                

                <b-col lg="2">SAA</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.saaName" placeholder="SAA" list="usersDiv"  v-on:change="getUsers"/> 
                </b-form-input></b-col> 
                

                <b-col lg="2">VP Education</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.vpeName" placeholder="VP Education" list="usersDiv"  v-on:change="getUsers"/> </b-form-input></b-col> 
                
                <b-col lg="2">President</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.presidentName" placeholder="VP Education" list="usersDiv"  v-on:change="getUsers"/> </b-form-input></b-col> 


                <b-col lg="2">Theme</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.theme"  placeholder="theme"/> </b-form-input></b-col> 
                <b-col lg="2">Date</b-col>
                <b-col lg="4"><b-form-input type="date" v-model="meeting.date"  placeholder="date"/> </b-form-input></b-col> 
                 <b-col lg="2">Time</b-col>
                <b-col lg="4"><b-form-input type="time" v-model="meeting.time"  placeholder="time"/> </b-form-input></b-col> 
                <b-col lg="2">Club name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.clubName" placeholder="Club name" list="autosuggestionDiv"  v-on:change="getAutosuggestion"/> </b-form-input></b-col>
                <b-col lg="2">Venue</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.venue" placeholder="Venue" list="autosuggestionDiv"  v-on:change="getAutosuggestion"/> </b-form-input></b-col> 
    </b-form>

    <br>
    <hr>
    <b-form inline>
            
            <b-col lg="3"><b-form-input type="text" v-model="speech_project" placeholder="speech project name"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_speaker_name" placeholder="speech speaker name" list="usersDiv" v-on:change="getUsers"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_evaluator_name" placeholder="speech evaluator name" list="usersDiv" v-on:change="getUsers"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="date" v-model="speech_date" placeholder="speech date"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_time_min" placeholder="min time"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_time_max" placeholder="max time"></b-form-input></b-col> 
    </b-form>
    <div align="center">
            <b-button variant="primary" v-on:click="addSpeech">Add speech</b-button>
    </div>
    

    <b-table striped hover small responsive=true stacked="md" :items="speech" :fields="speechTableFeilds" v-if="speech.length>0">

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
                searchMeetingNumber:"",
                speechTableFeilds:['id','meetingId','projectName', 'speakerName','speakerId','evaluatorName','evaluatorId','date','timeMin','timeMax','delete'],
                goalTableFeilds:['id','userId','userName','projectName','date','meetingId','delete'],
                users:[],
                userFetched:false,
                autosuggestion:[],
                autosuggestionFetched:false
              }
        },
        computed : {
            introductionSectionEndTime :  function(){
                if(this.meeting.time)
                    return addTime(this.meeting.time, 13 )
                 else
                     return addTime('00:00', 13 )   
              
            },
            PreparedSpeechEndTime :  function(){
                var sum=0;
                for(var i=0;i<this.speech.length;i++){
                    sum=parseInt(sum) + parseInt(this.speech[i].timeMax)+parseInt(1);
                }
                var totalTime= parseInt(sum) + parseInt(6); 
                return addTime(this.introductionSectionEndTime, totalTime); 
            },
            tableTopicsEndTime :  function(){
                return addTime(this.PreparedSpeechEndTime, 21);
            },
            evaluationEndTime : function(){
                var sum=0;
                for(var i=0;i<this.speech.length;i++){
                    sum=parseInt(sum) + parseInt(4);
                }
                var total = parseInt(sum)+ parseInt(22);
                return addTime(this.tableTopicsEndTime, total);
            }


        },
        created:function () {
        this.getAutosuggestion();
         this.getUsers();
        },
        methods: {
        getAutosuggestion(){
            if(this.autosuggestionFetched){
            return;
            }
            axios.get('https://mgtc.herokuapp.com/autosuggest/static')
              .then(response => {
                this.autosuggestion = response.data.data;
                this.autosuggestionFetched=true;
              })
            },
            getUsers(){
              if(this.userFetched){
               return;
              }
              axios.get('https://mgtc.herokuapp.com/users')
              .then(response => {
                this.users = response.data.data;
                this.userFetched=true;
              })
            },
            addOrUpdate(){
                axios
                    .post('https://mgtc.herokuapp.com/meetings/addOrUpdate',
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
                    .get('https://mgtc.herokuapp.com/meetings/'+this.searchMeetingNumber)
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
                window.location.href='http://mgtc.herokuapp.com/communication/agenda/'+this.searchMeetingNumber;
            }
        }
    }
     function    addTime(time,  minuteToAdd){
                var timeArray=time.split(':');
                   var hh= timeArray[0];
                   var mm= timeArray[1];
                   mm=parseInt(minuteToAdd)+parseInt(mm,10);
                   if(parseInt(mm,10)>=60){
                    mm=parseInt(mm,10) -60;
                    hh=parseInt(hh,10) +1;
                   }
                   if(parseInt(hh,10)>=24){
                    hh=parseInt(hh,10)-24;
                   }
                   var rs= hh+":"+mm;
                   return rs;
            }
</script>
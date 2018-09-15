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
    <datalist id=  "usersDiv">
        <option v-for="user in users">
        {{user}}
        </option>
    </datalist>
                <b-col lg="2">Meeting number</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.id" placeholder="meeting number"> </b-form-input></b-col> 
                <b-col lg="2">TTM name</b-col>
                <b-col lg="4">
                <b-form-input type="text" v-model="meeting.ttmName" placeholder="ttm name" list="usersDiv"/> 
                </b-form-input>
                </b-col> 
                <b-col lg="2">Grammarian name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.grammarianName"  placeholder="grammarian name" list="usersDiv"/> </b-form-input></b-col> 
                <b-col lg="2">Ah counter name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.ahCounterName"  placeholder="ah counter name" list="usersDiv"/> </b-form-input></b-col> 
                <b-col lg="2">TMOD name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.tmodName"  placeholder="tmod name" list="usersDiv"/> </b-form-input></b-col> 
                <b-col lg="2">Timer name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.timerName" placeholder="timer name" list="usersDiv"/> </b-form-input></b-col> 
                <b-col lg="2">GE name</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.geName" placeholder="GE name" list="usersDiv"/> </b-form-input></b-col> 
                <b-col lg="2">Theme</b-col>
                <b-col lg="4"><b-form-input type="text" v-model="meeting.theme"  placeholder="theme"/> </b-form-input></b-col> 
                <b-col lg="2">Date</b-col>
                <b-col lg="4"><b-form-input type="date" v-model="meeting.date"  placeholder="date"/> </b-form-input></b-col> 
                 <b-col lg="2">Time</b-col>
                <b-col lg="4"><b-form-input type="time" v-model="meeting.time"  placeholder="time"/> </b-form-input></b-col> 
    </b-form>

    <br>
    <hr>
    <b-form inline>
            
            <b-col lg="3"><b-form-input type="text" v-model="speech_project" placeholder="speech project name"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_speaker_name" placeholder="speech speaker name" list="usersDiv"></b-form-input></b-col> 
            <b-col lg="3"><b-form-input type="text" v-model="speech_evaluator_name" placeholder="speech evaluator name" list="usersDiv"></b-form-input></b-col> 
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
    <hr>
    <b-form inline>
        <b-col lg="4"><b-form-input type="text" v-model="goal_userName" placeholder="user name"/></b-col>
        <b-col lg="4"><b-form-input type="text" v-model="goal_projectName" placeholder="project name" list="usersDiv"/></b-col>
        <b-col lg="4"><b-form-input type="text" v-model="goal_date" placeholder="date"/></b-col>
        <b-col lg="4"><b-form-input type="text" v-model="goal_meeting_id" placeholder="meeting number"/></b-col>
    </b-form>
     <div align="center">
         <b-button variant="primary" v-on:click="addGoal">Add Goal</b-button>
    </div>
    <b-table striped hover small responsive=true stacked="md" :items="goal" :fields="goalTableFeilds" v-if="goal.length>0">
     <template slot="delete" slot-scope="row">
            <b-button size="sm" @click.stop="deleteGoal(row.index)">Delete</b-button>
    </template>
    </b-table>

    <br>
     <div align="center">
         <b-button variant="primary" v-on:click="addOrUpdate">Add/update Meeting</b-button>
    </div>

    <hr>
    <div v-if= "meeting.ttmName || meeting.grammarianName || meeting.ahCounterName || meeting.tmodName || meeting.timerName || meeting.geName || meeting.theme || speech.length>0 || goal.length>0">
    <div id="pdf">
        <b-container fluid>
        <b-row>
        <b-col cols="4" sm="2">
        <b-img-lazy center  src="/logo.png" fluid alt="Responsive image" />
        </b-col>
            <b-col>
                <div align="center">
                    <h3><b>{{clubName}}</b></h3>
                        <h5>
                Meeting # {{meeting.id}}<br>
                Date  :  {{meeting.date}}<br>
                Time  : {{meeting.time}}<br>
                Venue:  {{venue}}<br>
                </h5> <h3>
                Meeting Theme :<b> {{meeting.theme}}</b>
                </h3>
                        
                  </div>
            </b-col>
        </b-row>
        <b-row>
       <h4><b>Introduction Section ({{meeting.time}} - {{introductionSectionEndTime}}) </b><br> </h4>
       
        <table class="table table-bordered">
    <thead>
      <tr>
        <th class="col-xs-1">Time in minute</th>
        <th class="col-xs-2">Role player</th>
        <th class="col-xs-6">event</th>
        <th class="col-xs-3">Name of role player</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>1</td>
        <td>SAA</td>
        <td>Reading of Toastmaster's mission, general meeting guidance and handover to Presiding officer</td>
        <td>{{saa}}</td>
      </tr>
       <tr>
        <td>2</td>
        <td>Presiding Officer</td>
        <td>Welcome the audience, call guests to introduce and introduction of TMOD</td>
        <td>{{president}}</td>
      </tr>
       <tr>
        <td>2</td>
        <td>TMOD</td>
        <td>Brief on meeting structure, describe ballot and introduce word of the day and Introduce GE</td>
        <td>{{meeting.tmodName}}</td>
      </tr>
       <tr>
        <td>3</td>
        <td>GE</td>
        <td>Role description by GE, supplementary role players introduction and role description by each role player (Timer, Grammarian, Ah counter) and handing over the stage back to TMOD</td>
        <td>{{meeting.geName}}</td>
      </tr>
      <tr>
        <td>5</td>
        <td>TMOD</td>
        <td>Theme Presentation - Part 1</td>
        <td>{{meeting.tmodName}}</td>
      </tr>
     </tbody>
    </table>
    </b-row>
    <b-row>
    <h4><b>Prepared Speeches Section ({{introductionSectionEndTime}}-{{PreparedSpeechEndTime}} )</b></h4> 

    <table class="table table-bordered" v-if="speech.length>0">
        <thead>
        <tr>
            <th class="col-xs-1">Min time in minute</th>
            <th class="col-xs-1">max time in minute</th>
            <th class="col-xs-3">Speaker</th>
            <th class="col-xs-3">Evaluator</th>
            <th class="col-xs-4">Project Name</th>
        </tr>
        </thead>
        <tbody>
            <tr v-for="sp in speech">
                <td>{{sp.timeMin}}</td>
                <td>{{sp.timeMax}}</td>
                <td>{{sp.speakerName}}</td>
                <td>{{sp.evaluatorName}}</td>
                <td>{{sp.projectName}}</td>
            </tr>
            <tr v-for="go in goal">
                <td></td>
                <td></td>
                <td>{{go.userName}}</td>
                <td>{{go.evaluatorName}}</td>
                <td>{{go.projectName}}</td>
            </tr>
        </tbody>
    </table>
    <table class="table table-bordered">
    <thead>
      <tr>
        <th class="col-xs-1">Time in minute</th>
        <th class="col-xs-2">Role player</th>
        <th class="col-xs-6">event</th>
        <th class="col-xs-3">Name of role player</th>
      </tr>
    </thead>
    <tbody>
     <tr v-if="speech.length>0">
        <td>1</td>
        <td>SAA</td>
        <td>Voting for best speaker</td>
        <td>{{saa}}</td>
      </tr>
       <tr>
        <td>5</td>
        <td>TMOD</td>
        <td>Theme presentation Part 2</td>
        <td>{{meeting.tmodName}}</td>
      </tr>
    </tbody>
    </table>
    </b-row>
    <b-row>
    <h4><b>Table topics Section ({{PreparedSpeechEndTime}} - {{tableTopicsEndTime}})</b></h4> 
    <table class="table table-bordered">
    <thead>
      <tr>
        <th class="col-xs-1">Time in minute</th>
        <th class="col-xs-2">Role player</th>
        <th class="col-xs-6">event</th>
        <th class="col-xs-3">Name of role player</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>15</td>
        <td>TTM</td>
        <td>Table topics section</td>
        <td>{{meeting.ttmName}}</td>
      </tr>
      <tr>
        <td>1</td>
        <td>SAA</td>
        <td>Voting for best table topic speaker</td>
        <td>{{saa}}</td>
      </tr>
       <tr>
        <td>5</td>
        <td>TMOD</td>
        <td>Theme presentation Part 3</td>
        <td>{{meeting.tmodName}}</td>
      </tr>
    </tbody>
    </table>


    </b-row>
    <b-row>
    <h4><b>Evaluations Section ({{tableTopicsEndTime}}-{{evaluationEndTime}})</b></h4> 

    <table class="table table-bordered">
    <thead>
      <tr>
        <th class="col-xs-1">Time in minute</th>
        <th class="col-xs-7">event</th>
        <th class="col-xs-4">Name of role player</th>
      </tr>
    </thead>
    <tbody>
          <tr v-for="sp in speech">
            <td>4</td>
            <td>Evaluation of {{sp.speakerName}} for {{sp.projectName}}</td>
            <td>{{sp.evaluatorName}}</td>
          </tr>
          <tr>
            <td>4</td>
            <td>Timer report presentation</td>
            <td>{{meeting.timerName}}</td>
          </tr>     
          <tr>
            <td>4</td>
            <td>Ah counter report presentation</td>
            <td>{{meeting.ahCounterName}}</td>
          </tr>  
          <tr>
            <td>4</td>
            <td>Grammarian report presentation</td>
            <td>{{meeting.grammarianName}}</td>
          </tr>  
           <tr>
            <td>4</td>
            <td>GE report for overall meeting</td>
            <td>{{meeting.geName}}</td>
          </tr>  
           <tr>
            <td>1</td>
            <td>Voting for best evaluator, best role player and best supp role player by SAA</td>
            <td>{{saa}}</td>
          </tr>  
           <tr>
            <td>3</td>
            <td>Winners announcement and closing remarks by Presiding Officer</td>
            <td>{{president}}</td>
          </tr>  
          <tr>
            <td>2</td>
            <td>Request for next meeting roles</td>
            <td>{{vpe}}</td>
          </tr> 


    </tbody>
    </table>
    </b-row>

    </b-container>  
    </div>
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
    import jsPDF from 'jspdf'
    import html2canvas from 'html2canvas'
    window.html2canvas = html2canvas
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
                clubName:"Millenium Gurgaon Toastmasters club",
                saa:"Shyam Agrawal",
                president:"Sharad Maheshwari",
                vpe:"Anubhav Shrivastava",
                users:[ 'Ajay Pattanaik','Anjali Bajaj','Anubhav Shrivastava','Aritra Laha','Isha Sharma','Jitesh Pant','Lopamudra Mishra','Mohit Mendiratta','Mohit Dwivedi','Parul Bansal','Rajan Wadhwa','Rakhi Aswal','Sahil Sharma','Sanjeev Pathak','Sarika Kokadwar','Sharad Maheshwari','Shveta Gupta','Shyam Agrawal','Smita Narayan','Sundeep Rana','Vivek Sharma'],
                venue: 'PALLAVANJALI SCHOOL, 71, SHANTI STREET, BLOCK S, UPPAL SOUTHEND, SECTOR 49, GURUGRAM',
                time: '5 PM to 7 PM'
                
                
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
                var fileName= 'mgtc_'+this.meeting.id+'meeting_Agenda.pdf';
                html2canvas(document.getElementById("pdf")).then(function(canvas){
                        var img =  canvas.toDataURL("image/png",1.0);
                        
                         if(canvas.width > canvas.height){
                             var pdf = new jsPDF('l', 'mm', [canvas.width+40, canvas.height+40]);
                             pdf.addImage(img,'JPEG',20,20, canvas.width, canvas.height);
                             pdf.save(fileName);
                            }
                            else{
                            var pdf = new jsPDF('p', 'mm', [canvas.height+40, canvas.width+40]);
                             pdf.addImage(img,'JPEG',20,20, canvas.width, canvas.height);
                             pdf.save(fileName);
                            }
                         
                    }
                 )
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
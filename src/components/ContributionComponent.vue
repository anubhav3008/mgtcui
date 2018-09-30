<template>
    <div>
    <datalist id=  "usersDiv">
        <option v-for="user in users">
        {{user}}
        </option>
    </datalist>

 <b-form inline>
    <b-form-input type="text" placeholder="Name" v-model="name" list="usersDiv"/>
    <b-button variant="primary" v-on:click="getContribution">search</b-button>
    </b-form>
	
	</b-form>

	<b-table striped hover small responsive=true stacked="md" :items="contributionList.data"></b-table>
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
            name:"",
                contributionList:"",
                 users:[ 'Ajay Pattanaik','Anjali Bajaj','Anubhav Shrivastava','Aritra Laha','Isha Sharma','Jitesh Pant','Lopamudra Mishra','Mohit Mendiratta','Mohit Dwivedi','Parul Bansal','Rajan Wadhwa','Rakhi Aswal','Sahil Sharma','Sanjeev Pathak','Sarika Kokadwar','Sharad Maheshwari','Shveta Gupta','Shyam Agrawal','Smita Narayan','Sundeep Rana','Vivek Sharma']
                
              }
        },
        methods: {
            getContribution(){
      axios
      .get('http://localhost:8090/mgtc/users/contribution/byName/'+this.name)
      .then(response => {
      		alert('search complete');
      		this.contributionList = response.data;
      		})
      .catch(error => console.log(error))
            }
        }
    }
</script>

<template>
    <div>
    <datalist id=  "usersDiv">
        <option v-for="user in users" v-bind:value="user.name"  v-bind:label="user.name">
        </option>
    </datalist>

 <b-form inline>
    <b-form-input type="text" placeholder="Name" v-model="name" list="usersDiv"  v-on:change="getUsers"/>
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
                 users:[],
                 userFetched:false
                
              }
        },
        methods: {
            getContribution(){
      axios
      .get('https://srtmc-backend.azurewebsites.net/mgtc-1.0.0/users/contribution/byName/'+this.name)
      .then(response => {
      		alert('search complete');
      		this.contributionList = response.data;
      		})
      .catch(error => console.log(error))
            },
            getUsers(){
              if(this.userFetched){
               return;
              }
              axios.get('https://srtmc-backend.azurewebsites.net/mgtc-1.0.0/users')
              .then(response => {
                this.users = response.data.data;
                this.userFetched=true;
              })
            }
        },
        created:function () {
         this.getUsers();
        }
    }
</script>

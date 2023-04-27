<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

	<div  v-for="recentRecallInformation in recentRecallInformationList.records" :key="recentRecallInformation._id" class="recall-data">
		<div class="recall-title">
			<div>
				<span>{{recentRecallInformation.DT_ACCDN}}</span>
				<span class="location">{{recentRecallInformation.NB_VICTIMES_TOTAL}}</span>
			</div>
		</div>
	</div>
  </div>	
</template>

<script>
import axios from 'axios';

export default {
  name: 'HealthRecall',
  props: {
    msg: String
  }, 
	data() {
		return {
			recentRecallInformationList: [],
			languages: ['English', 'Français'],
			currentLanguage: 'English',
		};
	},


  created() {
	// fetch on init
	this.getRecentRecalls()
  },
  
    watch: {
    // re-fetch whenever currentBranch changes
    currentLanguage: 'getRecentRecalls'
  },

	methods: {
		getRecentRecalls() {
			const url = 'https://www.donneesquebec.ca/recherche/api/3/action/datastore_search?resource_id=ada44698-f402-49aa-8524-26d224e61b49&q=82025';
			
			axios.get(url).then(response => (this.recentRecallInformationList = response.data.result));
		}
	} 
  
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
recall-title {
  display: flex;
  align-items: center;
  margin-top: 20px;
  margin-left: 20px;
  border-bottom: 2px solid #ccc;
  padding: 20px;
}

button {
  padding: 10px;
  background-color: #1aa832;
  color: white;
  border: 1px solid #ccc;
}

li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

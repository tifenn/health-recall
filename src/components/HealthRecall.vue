<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

	<template v-for="language in languages" v-bind:key="language.id">
		<input type="radio"
		:id="language"
		:value="language"
		name="language"
		v-model="currentLanguage">		
		<label :for="language">{{ language}}</label>
	</template>
	
	
	<div  v-for="recentRecallInformation in recentRecallInformationList.HEALTH" :key="recentRecallInformation.recallId" class="recall-data">
		<div class="recall-title">
			<div>
				<span>{{recentRecallInformation.title}}</span>
				<span class="location">{{recentRecallInformation.category}}</span>
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
			const url = 'https://healthycanadians.gc.ca/recall-alert-rappel-avis/api/recent/' + (this.currentLanguage == 'English'? "en":"fr");
			
			axios.get(url).then(response => (this.recentRecallInformationList = response.data.results));
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

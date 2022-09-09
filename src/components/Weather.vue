<template>
	<!------Mobile Design--------->
	<div class="container bg-indigo-600 ">
		<div class="city">
			<h2 class="wild text-center text-white py-1 text-xl">Weather app</h2>
		</div>

		<div class="bracket w-full h-screen">
			
			<div class="">
				<input type="text" placeholder="Type in city" class="box border-gray-100 text-gray-100 text-lg rounded  block w-96 mx-auto p-3 dark:bg-gray-400 dark:border-gray-100 dark:placeholder-blue-900  shadow-lg"
				v-model="search"
				@keypress="getWeather">
			</div>

			<div class="innerItems text-center mt-20" v-if="typeof weather.main != 'undefined'">
				<div class="city my-3">
					<h4 class="text-indigo-500 text-lg font-bold">{{weather.name}}, {{weather.sys.country}}</h4>
				</div>

				<div class="date my-1">
					<h4 class="text-indigo-500 text-sm font-sm">{{dateUpdate()}}</h4>
				</div>

				<div class="degree">
					<h1 class="nums text-indigo-200">{{Math.round(weather.main.temp)}}<span class="text absolute my-11">o</span></h1>
				</div>

				<div class="status mt-2">
					<h3 class="text-indigo-500 font-sm text-xl">{{weather.weather[0].description}}</h3>
				</div>
			</div>
		</div>

	</div>
</template>

<style scoped>
.container {
	width: 100%;
}
.text{
	font-size: 25px;

}
.nums{
	font-size:150px;
}
.box{
	outline: none;
	margin-top: 80px;
}
.bracket{
	background-image: url(../assets/unsplash.jpg);
	position: absolute;

}

@media screen and (max-width: 380px){
.box{
	display: block;
	margin: 100px auto;
	width: 250px;
	}
}
@media screen and (min-width: 390px){
.box{
	display: block;
	margin: 120px auto;
	width: 400px;
	}
}


</style>

<script setup>
import { ref } from 'vue'
import axios from 'axios'


const search = ref(" ")
const weather = ref({})

const api_key = ref("d3c5ae1bb9a28dfe415667d9a5586119")
const url = ref("https://api.openweathermap.org/data/2.5/")

const getWeather = (e) => {
	if (e.key === 'Enter'){
		axios.get(`${url.value}weather?q=${search.value}&units=imperial&appid=${api_key.value}`)
	.then((res) => (weather.value = res.data));
	}
}

const dateUpdate = () => {
	const newDate = new Date();
	const months = ['January','February','March','April','May','June','June','July','August','September','October','November','December'];
	const days = ['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday','Sunday'];
	const day = days[newDate.getDay()];
	const date = newDate.getDate();
	const month = months[newDate.getMonth()];
	const year = newDate.getFullYear();

	return `${day} ${date} ${month} ${year}`

}
</script>
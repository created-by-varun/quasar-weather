<template>
  <q-page class="flex column">
  
  <!--============ Search section Start ============-->
  <div class="col q-pt-lg q-px-md">
  	<q-input
  	v-model="search"
  	placeholder="Search Location"
  	dark
  	borderless
  	>
  	
  	<template v-slot:before> 
  		<q-icon 
  		@click="getLocation"
  		name="my_location" />
  	</template>
  	
  	
  	<template v-slot:append> 
  		<q-btn round dense flat icon="search" />
  	</template>
  	</q-input>
	</div>
	<!--============ Search section End ============-->
	
	
	<template v-if="weatherData">
	
		<div class="col text-white text-center">
			<div class="text-h4 text-weight-light">
				{{ weatherData.name }}
			</div>
			<div class="text-h6 text-weight-light">
				{{ weatherData.weather[0].main }}
			</div>
			<div class="text-h1 text-weight-thin q-my-lg relative-position">
				<span>8</span>
				<span class="text-h4 relative-position degree">&deg;</span>
			</div>
			
		</div> 
		
		
		<div class="col text-center">
			<img src="" alt="weather-icon" />
		</div>
	</template>
	
	<template v-else>
		<div class="col column text-center text-white">
			<div class="col text-h2 text-weight-thin">
				Quasar <br> Weather
			</div>
			<q-btn class="col" flat> 
				<q-icon 
				left 
				@click="getLocation"
				size="3em" 
				name="my_location" />
				<div>Find my location</div>
			</q-btn>
		</div>
	</template>
	
	<div class="col skyline"> </div>
  
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data() {
  	return {
  		search: '',
  		weatherData: null,
  		lat: null,
  		lon: null,
  		apiUrl: 'https://api.openweathermap.org/data/2.5/weather',
  		apiKey: '4e5b5385f6fe76c0440b1f4d16e6b315'
  	}
  },
  methods: {
  	getLocation() {
  		navigator.geolocation.getCurrentPosition(position => {
  			this.lat = position.coords.latitude
  			this.lon = position.coords.longitude
  			this.getWeatherByCoords()
  		})
  	},
  	getWeatherByCoords() {
  		this.$axios(`${this.apiUrl}?lat=${this.lat}&lon=${this.lon}&appid=${this.apiKey}&units=metric`).then(response => {
  			this.weatherData = response.data
  		})
  	}
  }
}
</script>


<style lang="scss">
	.q-page{
		background: linear-gradient(to bottom, #136a8a, #267871);
	}
	.degree{
		top: -44px;
	}
	
	.skyline{
		flex: 0 0 100px;
		background: url(../statics/skyline.svg);
		background-size: contain;
		background-position: center bottom;
	}
		
	
	
</style>




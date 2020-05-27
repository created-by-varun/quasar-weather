<template>
  <q-page class="flex column">
  
  <div class="col q-pt-lg q-px-md">
  	<q-input
  	v-model="search"
  	placeholder="Search Location"
  	dark
  	borderless
  	>
  	
  	<template v-slot:before> 
  		<q-icon name="my_location" />
  	</template>
  	
  	
  	<template v-slot:append> 
  		<q-btn round dense flat icon="search" />
  	</template>
  	</q-input>
	</div>
	
	<div class="col text-white text-center">
		<div class="text-h4 text-weight-light">
			Bangalore
		</div>
	</div>
  
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data() {
  	return {
  		search: '',
  	}
  }
}
</script>


<style lang="scss">
	.q-page{
		background: linear-gradient(to bottom, #136a8a, #267871);
	}
</style>

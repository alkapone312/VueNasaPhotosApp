<template>
	<div class="item" :style="style"></div>
</template>

<script>
export default {

  name: 'Item',

  props: {
    item: {
      type: Object, // String, Number, Boolean, Function, Object, Array
      required: true,
    },
  },

  data () {
    return {
    	photo: this.item.links[0].href,
    	title: this.item.data[0].title,
    }
  },

  computed: {
  	style(){
    		return `background-image: url("${this.photo}")`
    	}
  }
}
</script>

<style lang="scss" scoped>
	.item
	{
		min-width: 70vw;
		height: 300px;
		background-size: cover;
		background-repeat: no-repeat;
		background-position: 50%;

		@media (min-width: 575px){
			min-width: 40vw;
			
		}

		@media (min-width: 768px) {
			min-width: 25vw;
		}

		@media (min-width: 1500px) {
			min-width: 20vw;
		}
	}
</style>
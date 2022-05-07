<template>
		<input 
			type="text" 
			name="search" 
			:value="value"
			@input="handleChange"
			:class="{dark}"
		/>
</template>

<script>
export default {

  name: 'Search',

  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
    	type: Boolean,
    	default: false,
    }
  },

  methods: {
    handleInput (e) {
      this.$emit('input', e.target.value)
    }
  },

  data () {
    return {

    }
  },
}
</script>

<style lang="scss" scoped>
input{
	margin-top: 50px;
	display: flex;
	flex-direction: column;
	width: 250px;
	text-align: center;
	font-size: 18px;
	font-weight: 300;
	color: #fff;
	height: 30px;
	border: 0;
	border-bottom: 1px solid white;
	background: none;
	transition:box-shadow .5s;

	@media (min-width: 1024px){
		font-weight: 400;
	}
}

input:focus{
	outline: none;
	box-shadow: 0 10px 15px -8px rgba(255,255,255,0.4);

}

.dark
{
	color:#1e3d4a;
	border-bottom-color: #1e3d4a;
}

.dark:focus {
	box-shadow: 0 10px 20px 8px rgba(#1e3d4a, 0.2);
}
</style>
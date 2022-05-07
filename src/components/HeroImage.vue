<template>
	<div class="heroImage"></div>
</template>

<script>
export default {

  name: 'HeroImage',

  data () {
    return {

    }
  }
}
</script>

<style lang="scss" scoped>

.heroImage{
	position: fixed;
	top: 0;
	left: 0;
	z-index: -1;
	width: 100%;
	height: 100vh;
	background: linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4)), url('../assets/heroImage.jpg');
	background-size: cover;
	background-repeat: no-repeat;
}

</style>
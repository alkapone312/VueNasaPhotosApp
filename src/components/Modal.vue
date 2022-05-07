<template>
	<div class="outerWrapper">
		<div class="innerWrapper">
			<div class="photo">
				<img :src="item.links[0].href" alt="Image">
			</div>
			<div class="description">
				<h2 class="title">
					{{item.data[0].title}}
				</h2>
				<p>
					{{item.data[0].description}}
				</p>
			</div>
		</div>
		<div class="close" @click="$emit('closeModal')"></div>
	</div>
</template>

<script>
export default {

  name: 'Modal',

  props: {
    item: {
      type: Object,
      required: true,
    }
  },

  data () {
    return {

    }
  },
}
</script>

<style lang="scss" scoped>
	.outerWrapper{
		background-color: #f6f6f6;
		height: 100%;
		max-width: 100%;
		position: fixed;
		top: 0;
		left: 0;

		@media (min-width: 1024px) {
			max-width: 70%;
			height: 60%;
			left: 0;
			right: 0;
			top: 0;
			bottom: 0;
			margin: auto;
			box-shadow: 0 30px 30px -10px rgba(0, 0, 0, 0.3);
		}
	}

	.innerWrapper{
		display: flex;
		width: 100vw;
		height: 100%;
		padding: 50px;
		justify-content: center;
		align-items: center;
		flex-direction: column;

		@media (min-width: 1024px) {
			flex-direction: row;
			width: 100%;
			height: 100%;

			.photo {
				width: 100%;
				height: 100%;
				margin-right: 20px;
			}
		}

		.photo {
			width: 100%;
			max-height: 100%;
			background-color: #000;
			overflow: hidden;

			img {
				width: 100%;
				object-fit: contain;
			}
		}
	}

	.description {
		color: #333;
		width: 100%;
		max-height: 80%;;
		overflow: scroll;
	}

	.close
	{
		padding: auto;
		width: 30px;
		height: 30px;
		padding: 30px;
		right: 0;
		top: 0;
		cursor: pointer;

		&::before,
		&::after {
			position: absolute;
			top: 30px;
			right: 20px;
			content: '';
			width: 20px;
			height: 2px;
			background-color: #000;
			display: block;
		}

		&::before {
			transform: rotate(45deg);
		}
		&::after {
			transform: rotate(-45deg);
		}
	}
</style>
<template>
	<footer id="footer">
		<div class="kudos">
			<p>Special thanks to Nintendo&trade;</p>
			<p>Made by <a href="http://spenserpeiffer.com" target="_blank">Spenser Peiffer</a> | View the <a href="https://github.com/speiffer829/critterpedia" target="_blank">Github</a></p>
		</div>
	</footer>
</template>


<script>
export default {
	name:"Footer"
}
</script>


<style lang="scss">
@import '@/assets/global.scss';
	footer{
		color: $tan;
		font-family: $headFont;
		text-shadow: 2px 2px 5px #005524;
		text-align: center;
		font-size: 0.8rem;
		backdrop-filter: blur(3px);
		padding: 0.8rem;

		a{
			color: $tan;
			font-style: italic;

			&:hover{
				color: $gold;
			}
		}
	}
</style>
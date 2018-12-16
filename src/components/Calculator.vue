<template>
	<div id="calc-wrapper">
		<h1 id="display">{{ displayValue }}</h1>
		<div id="buttons-wrapper">
			<CalcBtn :value="1"></CalcBtn>
			<CalcBtn :value="2"></CalcBtn>
			<CalcBtn :value="3"></CalcBtn>
			<CalcBtn :value="4"></CalcBtn>
			<CalcBtn :value="5"></CalcBtn>
			<CalcBtn :value="6"></CalcBtn>
			<CalcBtn :value="7"></CalcBtn>
			<CalcBtn :value="8"></CalcBtn>
			<CalcBtn :value="9"></CalcBtn>
			<CalcBtn :value="0"></CalcBtn>
		</div>
	</div>
</template>

<script>
import CalcBtn from './CalcBtn.vue'
export default {
	name: 'Calculator',
	components: {
		CalcBtn
	},
	data() {
		return {
			displayValue:0
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#calc-wrapper{
	text-align: center;
	margin: 30px auto;
	width: 900px;
}

#display {
	background-color: #35495e;
	color: white;
	height: 100px;
	line-height: 100px;
	margin:0px;
}

#buttons-wrapper {
	display: grid;
	grid-template-columns: repeat(3, 1fr);
}
</style>

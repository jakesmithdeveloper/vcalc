<template>
	<div id="calc-wrapper" @mouseup="mouseUp">
		<h1 id="display">{{ display }}</h1>
		<div id="buttons-wrapper">
			<CalcBtn :isOp="true" value="C"></CalcBtn>
			<CalcBtn :isOp="true" value="*"></CalcBtn>
			<CalcBtn :isOp="true" value="/"></CalcBtn>
			<CalcBtn :isOp="true" value="(-)"></CalcBtn>
			<CalcBtn :isOp="false" value="1"></CalcBtn>
			<CalcBtn :isOp="false" value="2"></CalcBtn>
			<CalcBtn :isOp="false" value="3"></CalcBtn>
			<CalcBtn :isOp="true" value="+"></CalcBtn>
			<CalcBtn :isOp="false" value="4"></CalcBtn>
			<CalcBtn :isOp="false" value="5"></CalcBtn>
			<CalcBtn :isOp="false" value="6"></CalcBtn>
			<CalcBtn :isOp="true" value="-"></CalcBtn>
			<CalcBtn :isOp="false" value="7"></CalcBtn>
			<CalcBtn :isOp="false" value="8"></CalcBtn>
			<CalcBtn :isOp="false" value="9"></CalcBtn>
			<CalcBtn :isOp="true" value="Enter"></CalcBtn>
			<CalcBtn :isOp="false" value="0"></CalcBtn>
		</div>
	</div>
</template>

<script>
import CalcBtn from './CalcBtn.vue'
import { EventBus } from '../main'

export default {
	name: 'Calculator',
	components: {
		CalcBtn
	},
	data() {
		return {
			display: '0',
			appendingMode: false,
			operationData: {
				leftOperand: 0,
				op: null
			}
		}
	},
	computed: {
		displayValue: function() {
			return Number(this.display);
		}
	},
	methods: {
		mouseUp() {
			EventBus.$emit('mouse-up', false);
		},
		handleDigit(digit) {
			if (this.appendingMode) {
				this.display += digit;
			} else {
				this.display = digit
				this.appendingMode = true;
			}
		},
		handleOp(op) {
			if (op == 'C') {
				this.display = '0';
				this.opDataReset();
				this.appendingMode = false;
			} else if (op == '+' || op == '-' || op == '/' || op == '*') {
				if(this.operationData.op == null) {
					// This number should be the first operand
					this.operationData.leftOperand = this.displayValue;
					this.operationData.op = op;
				} else {
					// perform operation and set up for next operation
					const tempOp = op;
					this.handleOp('Enter');
					this.handleOp(tempOp);
				}
			} else if (op == 'Enter') {
				const operation = this.operationData.op;
				if (operation === null) {
					console.log('ERROR no operation selected');
				} else {

					const leftOperand = this.operationData.leftOperand;
					const rightOperand = this.displayValue;

					switch (operation) {
						case '+':
							this.display = (leftOperand + rightOperand).toString();
							break;
						case '-':
							this.display = (leftOperand - rightOperand).toString();
							break;
						case '*':
							this.display = (leftOperand * rightOperand).toString();
							break;
						case '/':
							this.display = (leftOperand / rightOperand).toString();
							break;
						default:
							break;
					}
					// reset the operation data for the next operation
					this.opDataReset();
				}
			}
		},
		opDataReset() {
			this.operationData.leftOperand = 0;
			this.operationData.op = null;
		}
	},
	mounted() {
		EventBus.$on('button-pressed', (btn) => {
			if (btn.isOp) {
				// operation
				this.appendingMode = false;
				this.handleOp(btn.value);
			} else {
				// digit
				this.handleDigit(btn.value);
			}
		});
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
	grid-template-columns: repeat(4, 1fr);
}
</style>

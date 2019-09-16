<template>
	<input type="text" v-model="inputVal" v-on:keypress="isNumber()" v-on:keyup="checkComma()">
</template>
<script type="text/javascript">
/**
 * CodersStudio 2019
 * https://coders.studio
 * info@coders.studio
 */
export default {
	name: 'Number',
	props: {
		decimalPlaces: {
			default: 2
		},
		'value'
	},
	data(){
		return  {
			inputVal: this.value,
			isComma:false
		}
	},
	watch: {
		inputVal(val) {
			this.$emit('input', val);
		}
	},
	methods: {
		isNumber: function() {
			let number = String(this.inputVal);
			const {event} = window;
			let evt = event;
			let charCode = (evt.which) ? evt.which : evt.keyCode;
			if (
					(charCode > 31 && (charCode < 48 || charCode > 57))
					&& charCode !== 44
					&& charCode !== 46
					|| (this.isComma && charCode == 44)
					|| (number.indexOf(",")>0 && number.length-number.indexOf(",")>this.decimalPlaces)
			) {
				evt.preventDefault();
			} else {
				return true;
			}
		},
		checkComma: function() {
			let number = String(this.inputVal);
			if(number.indexOf(".")>=0){
				if(number.indexOf(",")<0) number = number.replace('.', ',');
				else number = number.replace('.', '');
			}
			this.inputVal = number;
			this.isComma = number.indexOf(",") >= 0;
			return true;
		}
	}
}
</script>

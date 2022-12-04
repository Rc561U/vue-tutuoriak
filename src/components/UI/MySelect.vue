<template>
	<select v-bind:value="modelValue" @change="changeOption">
		<option disable value="">Choice option from list</option>
		<option v-for="option in options" :key="option.value" :value="option.value">
			{{ option.name }}
		</option>
	</select>
		
</template>
<script>
export default {
	name:'my-select',
	props: {
		modelValue: {
			type: String
		},

		options: {
			type: Array,
			default: () => []
		}
	},
	methods: {
		changeOption(event) {
			this.$emit('update:modelValue', event.target.value);
		}
	}
}
</script>
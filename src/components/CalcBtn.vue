<template>
  <div>
    <span>{{ value }}</span>
  </div>
</template>

<script>
export default {
  name: 'CalcBtn',
  props: {
	  value: {
		  type: Number,
		  required: true
	  }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

<template>
  <div @mousedown="isClicked=true" @mouseup="isClicked=false" :class="{buttonDown:isClicked}">
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
  },
  data() {
    return {
      isClicked: false
    }
  }
}
</script>

<style scoped>
  div{
    background-color: #42b883;
    color: white;
    height: 64px;
    line-height: 64px;
    margin: 10px;
  }

  div span {
    user-select: none;
  }

  .buttonDown {
    background-color: black;
    color: white;
    height: 64px;
    line-height: 64px;
    margin: 10px;
  }
</style>

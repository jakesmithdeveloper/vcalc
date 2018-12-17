<template>
  <div @mousedown="buttonPressed" @mouseup="isClicked=false" :class="{buttonDown:isClicked,opBtn: isOp}">
    <span>{{ value }}</span>
  </div>
</template>

<script>
import { EventBus } from '../main'

export default {
  name: 'CalcBtn',
  props: {
	  value: {
		  type: String,
		  required: true
    },
    isOp: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      isClicked: false
    }
  },
  methods: {
    buttonPressed() {
      this.isClicked = true;
      EventBus.$emit('button-pressed', this);
    }
  },
  created() {
    EventBus.$on('mouse-up', () => {
      this.isClicked = false;
    });
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

  .opBtn {
    background-color: #ff695e;
    color: white;
    height: 64px;
    line-height: 64px;
    margin: 10px;
  }

  .buttonDown {
    background-color: black;
    color: white;
    height: 64px;
    line-height: 64px;
    margin: 10px;
  }
</style>

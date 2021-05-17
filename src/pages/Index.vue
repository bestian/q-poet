<template>
  <q-page class="flex flex-center flex-reversed">
    <p v-for="d in data" :key="d">
     <span v-for = "t in d.split('')" :key="t" >
    	<box :w = "t"></box>
     </span>
    </p>
  </q-page>
</template>

<script>

import Box from '../components/Box.vue'

export default {
  name: 'PageIndex',
  components: { 
  	Box,
  },
  data () {
  	return {
  		data: null
  	}
  },
  mounted() {
  	this.$axios.get('https://bestian.github.io/q-poet/poets/床前明月').then((r) => {
  		this.data = r.data.split('\n')
  	})
  }
}
</script>

<style type="text/css" scoped="">

.flex-reversed {
	flex-flow: row-reverse;
}

p {
  -webkit-writing-mode: vertical-rl;
  -ms-writing-mode: tb-rl;
  writing-mode: vertical-rl;
  white-space: pre-line;
  font-size: 24px;
  line-height: 2em;
  height: 90vh;
  padding: 0.5em 0;
}
</style>

<template>
  <q-page class="flex flex-center flex-reversed">
    <q-input class="no-print" filled
      type="textarea" name="ip" v-model="ip"/>
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
  		data: null,
      ip: '',
  	}
  },
  mounted() {
  	this.data = this.ip.split('\n')
  },
  watch: {
    ip: function (val) {
       this.data = val.split('\n')
    },
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

<template>
  <q-page id="main" class="flex flex-center flex-reversed">
  	<q-select v-model="s" :options="options" >
  	</q-select>
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
  		s: '床前明月',
  		data: null,
  		options: ['床前明月', '將進酒']
  	}
  },
  mounted() {
  	this.$axios.get('https://bestian.github.io/q-poet/poets/床前明月').then((r) => {
      var list = r.data.split('')
      for (var i = 0; i < list.length; i++) {
        if (list[i] == '，' || list[i] == '。') {
          list[i] = list[i] + '\n'
        }
      }
      var x = list.join('')
  		this.data = x.split('\n')
  	})
  },
  watch: {
  	s: function (val) {
  		this.$axios.get('https://bestian.github.io/q-poet/poets/' + val).then((r) => {
  		this.data = r.data.split('\n')
	  })
  	}
  }
}
</script>

<style type="text/css" scoped="">

.flex-reversed {
	flex-flow: row-reverse;
	overflow-x: scroll;
}

p {
  -webkit-writing-mode: vertical-rl;
  -ms-writing-mode: tb-rl;
  writing-mode: vertical-rl;
  white-space:nowrap;
  height: 85vh;
  padding: 0em 0;
  overflow-y: auto;
  overflow-x: hidden;
  margin-right: -1.6em; 
}

#main {
	position: absolute;
  z-index: 999;
	top: 6em;
	right: 0;
  height: 85vh;
  width: 66vw;
  overflow-x: scroll;
}
</style>

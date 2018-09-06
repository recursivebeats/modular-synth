<template>
  <div id="app" @keydown="triggerTestSynth($event)">
    <div class="main-synth">
      <div class="component-row" v-for="(row, i) in 3" :key="i">
        <div class="component-column" v-for="(col, j) in 3" :key="j">
            <SynthComponent :position="`${i+1}${j+1}`" :name="`module${i+1}${j+1}`"/>
        </div>
      </div>
    </div>
    <div class="test-synth" >

    </div>
    <input style="display: none;" autofocus @keydown="triggerTestSynth($event)">
  </div>
</template>

<script>
import SynthComponent from './components/SynthComponent.vue'
import Tone from 'tone'
export default {
  name: 'app',
  components: {
    SynthComponent
  },
  data() {
    return {
      keys: { }
    }
  },
  methods: {
    triggerTestSynth(e){
      console.log(e)
    },
    handleKeyEvent(event) {
      this.keys[event.key] = event
      this.$store.dispatch('keyPress/editKeyPress', this.keys)
    }
  },
  created () {
    addEventListener('keydown', function(event){
      let eventObj = {
        active: true,
        key: event.key
      }
      // console.log(eventObj)
      // console.log(this)
    })

    addEventListener('keyup', function(event){
      let eventObj = {
        active: false,
        key: event.key
      }
      //this.handleKeyEvent(eventObj)
    })
  }
}
</script>

<style>

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100%;
  height: 100%;
  display: inline-grid;
  grid-template-columns: 1fr 880px 1fr;
  grid-template-rows: 1fr 880px 1fr;
}

.test-synth {

}
.debug-window {
  background: grey;
  color: white;
  grid-row: 1/4;
  grid-column:1/2;
  display: inline-grid;
  grid-template-rows: repeat(auto-fit, 1fr);
  font-size: 0.8rem;
}
.debug-window p{
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center
}

.debug-module {
  border: 1px dashed white;
}

.main-synth {
  grid-row: 2/3;
  grid-column: 2/3;
  background: white;
  display: inline-grid;
  grid-template-rows: repeat(3, 1fr);
}

.component-row {
  display: inline-grid;
  grid-template-columns: repeat(3, 1fr);
}

</style>

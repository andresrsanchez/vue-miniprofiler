<template>
  <div id="app">
    <MiniProfiler 
      :scriptSrc="scriptSrc"
      :dataPath="dataPath"
      :cssSrc="cssSrc"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './components/HelloWorld.vue';
import MiniProfiler from './components/MiniProfiler.vue';
import axios from 'axios';

@Component({
  components: {
    HelloWorld,
    MiniProfiler,
  },
})
export default class App extends Vue {
  private scriptSrc: string = 'http://localhost:5000/mini-profiler-resources/includes.min.js';
  private dataPath: string = 'http://localhost:5000/mini-profiler-resources/';
  private cssSrc: string = 'http://localhost:5000/mini-profiler-resources/includes.min.css';
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

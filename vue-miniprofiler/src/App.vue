<template>
  <div id="app">
    <MiniProfiler 
      :scriptSrc=lol
      
       />
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
  private created() {
    const key: string = 'MiniProfiler';
    const miniProfiler: any = (window as any)[key];
    console.log(miniProfiler);

    axios.interceptors.response.use(function lel(config) {
      const miniProfilerIds = JSON.parse(config.headers['x-miniprofiler-ids']) as string[];
      miniProfiler.fetchResults(miniProfilerIds);
      console.log(config);
      return config;
    }, function lol(error) {
      console.log(error);
      return Promise.reject(error);
    });
  }
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

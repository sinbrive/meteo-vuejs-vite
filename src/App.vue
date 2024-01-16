<template>
  <h1>Hello Météo Vue JS</h1>
  <GetAPI @data_received="handleData"/>
  <div v-if="json">
    <Display :data='json' :icon_path='icon' />
  </div>
</template>

<script>
 import GetAPI from './components/GetAPI.vue'
 import Display from './components/Display.vue'
 import "./assets/main.css";
  
export default {
  name: 'App',
  components: {
   GetAPI,
   Display
  },
  data() {
    return {
      json: null,
      icon: null
    };
  },
  methods:{
    handleData(d){
      this.json=d.data;
      this.icon=d.path;
    },
  },

}
</script>

<style>

</style>

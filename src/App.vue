<template>  
  <div tabindex="0" class="project">
    <p class="selected-tool">selected tool is: <span class="selected-name">hand</span></p>
    <toolbar @itemSelected="itemSelected"/>
  </div>
</template>

<script>

import toolbar from './components/toolbar.vue'
import $ from 'jquery';

export default {
  name: 'App',
  components: {    
    toolbar
  },
  methods:{
      itemSelected(e){
        $('p.selected-tool .selected-name').text(e)
      }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

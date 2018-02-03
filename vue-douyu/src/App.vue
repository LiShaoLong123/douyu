<template>
  <div id="app">
    
    <transition name="sideMenuAni">
    	<SideMenu @hideMenu="hideMenu" v-show="showSideMenu"></SideMenu>
    </transition>
    
    <transition name="back">
    	<router-view></router-view>
    </transition>
    
    
    
    
  </div>
</template>

<script>

import SideMenu from "./components/SideMenu";
import bus from "./bus.js";

export default {
  name: 'app',
  components:{
  	SideMenu:SideMenu
  },
  data:function(){
  	return {
  		showSideMenu:false
  	}
  },
  methods:{
  	hideMenu:function(){
  		this.showSideMenu = false;
  	},
  	showMenu:function(){
  		this.showSideMenu = true;
  	}
  },
  mounted:function(){
		bus.$on("menuClick",this.showMenu);
		
  }
}
</script>

<style scoped>
	.sideMenuAni-enter-active,.sideMenuAni-leave-active{
		transition: all 0.5s;
	}
	.sideMenuAni-enter,.sideMenuAni-leave-active{
		opacity: 0;
		transform: translateX(-100%);
	}
	
	.back-enter-active,.back-leave-active{
		transition: all 0.5s;
	}
	.back-enter,.back-leave-active{
		transform: translateX(100%);
	}
	.back-leave{
		transform: translateX(-100%);
	}
	
</style>

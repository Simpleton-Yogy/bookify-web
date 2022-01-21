<template>
  <div class="mainContainer">
    <div class="menuContainer">
      <div class="menuLogoContainer">
        <div class="menuLogoText">Bookify</div>
      </div>
      <div class="menuItemsContainer">
        <MenuItem text = "Home" icon = "homeIcon" value = "home" :toggledItem = "selectedMenuItem" @click="onMenuItemClick" />
        <MenuItem text = "Library" icon = "libraryIcon" value = "library" :toggledItem = "selectedMenuItem" @click="onMenuItemClick" />
        <MenuItem text = "Search" icon = "searchIcon" value = "search" :toggledItem = "selectedMenuItem" @click="onMenuItemClick" />
        <MenuItem text = "Settings" icon = "settingsIcon" value = "settings" :toggledItem = "selectedMenuItem" @click="onMenuItemClick" />
      </div>
    </div>
    <div class="contentContainer">
      <transition-group name="slide-fade">
        <Home v-if="selectedMenuItem == 'home'"/>
        <Search v-if="selectedMenuItem == 'search'"/>
      </transition-group>
    </div>
  </div>
</template>

<script>

// Import Pages
import Home from '@/pages/Home.vue';
// import Library from '@/pages/Library.vue';
import Search from '@/pages/Search.vue';
// import Settings from '@/pages/Settings.vue';

// Import Components
import MenuItem from '@/components/MenuItem.vue';

export default {
  name: 'App',
  components: {
    MenuItem, Home, Search
  },
  data: function() {
    return {
      selectedMenuItem: 'home',
    }
  },
  methods: {
    onMenuItemClick: function(value) {
      if (typeof value !== "object"){
        if (value !== this.selectedMenuItem){
          this.selectedMenuItem = value
        }
      }
    }
  }
}
</script>

<style lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,100;1,200;1,300;1,400;1,500;1,600;1,700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Lobster&display=swap');
@import "@/assets/colors.scss";

#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: $text;
}

body {
  margin: 0;
  padding: 0;
  overflow: hidden;
}

.mainContainer {
  width: 100vw;
  min-height: 100vh;
  display: flex;
  flex-flow: row nowrap;
  justify-content: stretch;
  margin: 0;
  padding: 0;

  .menuContainer {
    width: 15%;
    display: flex;
    flex-flow: column nowrap;
    justify-content: flex-start;
    align-items: stretch;
    background-color: $dark;

    .menuLogoContainer {
      display: flex;
      flex-flow: column nowrap;
      align-items: center;
      justify-content: stretch;

      .menuLogoText {
        font-size: 42px;
        font-family: 'Lobster', cursive;
        margin: 20px 0;
      }
    }

    .menuItemsContainer {
      display: flex;
      flex-flow: column nowrap;
      justify-content: center;
      align-items: center;
      background-color: $dark;
      padding: 0 40px 0 0;
    }
  }

  .contentContainer {
    width: 85%;
    display: flex;
    flex-flow: column nowrap;
    justify-content: flex-start;
    align-items: flex-end;
    background-color: $light;
  }
  
}

.slide-fade-enter-active {
  animation: slide-fade-animation reverse 220ms 220ms ease-in-out;
}

.slide-fade-leave-active {
  animation: slide-fade-animation 220ms ease-in-out;
}

.slide-fade-enter {
  opacity: 0;
  transform: translateX(30px);
}

@keyframes slide-fade-animation {
  from {
    opacity: 1;
    transform: translateX(0px);
  }

  to {
    opacity: 0;
    transform: translateX(30px);
  }
}

.fade-enter-active {
  animation: fade-animation reverse 260ms ease-in-out;
}

.fade-leave-active {
  animation: fade-animation 260ms ease-in-out;
}

@keyframes fade-animation {
  from {
    opacity: 1;
  }

  to {
    opacity: 0;
  }
}


</style>

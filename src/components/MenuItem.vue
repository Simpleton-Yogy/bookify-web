<template>
    <div class="menuItemContainer" @click="clicked">
        <div class="menuItemColorBar" :class="{menuItemBarToggled: toggled}" />
        <div class="menuItemContent">
            <img class="menuItemIcon" :src = "require(`@/assets/${icon}.svg`)" />
            <div class="menuItemText">{{ text }}</div>
        </div>
    </div>
</template>


<script>

export default {
  name: 'MenuItem',
  components: {
  },
  props: {
      'text': String,
      'value': String,
      'icon': String,
      'toggledItem': String
  },
  methods: {
      clicked: function() {
          this.$emit("click", this.value);
      }
  },
  data: function(){
      return {
          toggled: this.toggledItem === this.value
      }
  },
  watch: {
      toggledItem: function(){
          this.toggled = this.toggledItem === this.value
      }
  }
}
</script>


<style scoped lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,100;1,200;1,300;1,400;1,500;1,600;1,700&display=swap');
@import "@/assets/colors.scss";

.menuItemContainer {
    width: 100%;
    display: flex;
    flex-flow: row nowrap;
    align-items: center;
    justify-content: flex-start;
    margin: 10px 0 20px 0;
    cursor: pointer;

    &:hover > .menuItemColorBar {
            animation: barHoverAnimation;
            animation-duration: 220ms;
            animation-timing-function: ease-in-out;
            margin-right: -100%;
            width: 100%;
            border-radius: 0 5px 5px 0;
        }
    
    .menuItemColorBar {
        height: 58px;
        width: 0%;
        margin: -10px -0% -10px 0;
        background-color: $blue;
        z-index: 1;
        transition: all 220ms ease-in-out;
    }

    .menuItemContent {
        width: 100%;
        height: 100%;
        display: flex;
        flex-flow: row nowrap;
        justify-content: flex-start;
        align-items: center;
        padding: 8px 0;
        border-radius: 0 5px 5px 0;
        background-color: $light;
        transition: all 220ms ease-in-out;

        .menuItemIcon {
            height: 20px;
            width: auto;
            margin: 0 10px 0 40px;
            z-index: 2;
        }

        .menuItemText {
            color: $text;
            font-family: 'Montserrat', sans-serif;
            font-size: 18px;
            font-weight: 600;
            z-index: 2;
        }
    }
}

.menuItemBarToggled {
    width: 100% !important;
    margin-right: -100% !important;
    border-radius: 0 5px 5px 0;
}

@keyframes barHoverAnimation {
    from {
        width: 0%;
        margin-right: -0%;
        border-radius: 0px 5px 5px 0px;
    }

    to {
        width: 100%;
        margin-right: -100%;
        border-radius: 0px 5px 5px 0px;
    }
}

</style>

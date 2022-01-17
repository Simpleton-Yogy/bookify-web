<template>
    <div class="menuItemContainer">
        <input type="radio" class="menuItemFunctional" name = "menu" />
        <div class="menuItemDummy">
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
      'icon': String
  }
}
</script>

<style scoped lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,100;1,200;1,300;1,400;1,500;1,600;1,700&display=swap');
@import "@/assets/colors.scss";

.menuItemContainer{
    width: 100%;
    display: flex;
    flex-flow: column nowrap;
    align-items: center;
    justify-content: center;
    margin: 10px 0 20px 0;
    
    .menuItemFunctional {
        width: 100%;
        height: 42px;
        margin: 0 0 -42px 0;
        z-index: 1;
        opacity: 0;
        cursor: pointer;

        &:checked + .menuItemDummy {
            background-color: $blue;
        }
    }

    .menuItemDummy {
        width: 100%;
        height: 100%;
        z-index: 0;
        display: flex;
        flex-flow: row nowrap;
        justify-content: flex-start;
        align-items: center;
        padding: 8px 0;
        border-radius: 0 5px 5px 0;
        background-color: $light;
        transition: all 250ms ease-in-out;

        .menuItemIcon {
            height: 20px;
            width: auto;
            margin: 0 10px 0 40px;
        }

        .menuItemText {
            color: $text;
            font-family: 'Montserrat', sans-serif;
            font-size: 18px;
            font-weight: 600;
        }
    }
}

</style>

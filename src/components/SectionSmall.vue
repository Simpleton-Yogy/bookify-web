<template>
    <transition name="slide-fade">
        <div class="sectionContainer" v-if="!!$slots.default">
            <div class="sectionTitle">{{ title }}</div>
            <div class="sectionContent">
                <slot></slot>
            </div>
        </div>
    </transition>
</template>

<script>


export default {
  name: 'SectionSmall',
  components: {
    
  },
  props: [
      'title'
  ]
}


</script>

<style scoped lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,100;1,200;1,300;1,400;1,500;1,600;1,700&display=swap');
@import "@/assets/colors.scss";

.sectionContainer {
    display: flex;
    flex-flow: column nowrap;
    justify-content: center;
    align-items: flex-start;
    padding: 30px 0 20px 50px;
    background-color: $dark;
    border-radius: 10px 0 0 10px;
    margin-bottom: 5%;

    .sectionTitle {
        color: $text;
        font-family: 'Montserrat', sans-serif;
        font-size: 35px;
        font-weight: 700;
        margin: 0 0 15px -20px;
    }

    .sectionContent {
        display: flex;
        flex-flow: row nowrap;
        justify-content: flex-start;
        align-items: center;
        overflow-x: auto;
        min-height: 100px;
        width: 100%;

        &::-webkit-scrollbar {
            height: 8px;
        }

        &::-webkit-scrollbar-track {
            height: 10px;
            background-color: $light;
            border-radius: 2px;
        }

        &::-webkit-scrollbar-thumb {
            height: 6px;
            background-color: $blue;
            border-radius: 2px;
            margin: 2px
        }
    }
}

</style>

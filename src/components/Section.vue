<template>
    <div class="sectionContainer">
        <div class="sectionTitle">{{ title }}</div>
        <div class="sectionContent" v-bind:class = "{bigSection : bigSectionSelected, smallSection : smallSectionSelected}">
            {{ content }}
        </div>
    </div>
</template>

<script>


export default {
  name: 'MenuItem',
  components: {
    
  },
  props: [
      'title', 'content', 'style'
  ],

  data: function () {

      let smallSection = false;
      let bigSection = false;

      if (this.style === "small"){
          smallSection = true;
      }
      else if (this.style === "big"){
          bigSection = true;
      }

      return {
          bigSectionSelected: bigSection,
          smallSectionSelected: smallSection
      }
  }
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
    padding: 20px 0 20px 20px;
    background-color: $dark;
    border-radius: 10px 0 0 10px;

    .sectionTitle {
        color: $text;
        font-family: 'Montserrat', sans-serif;
        font-size: 35px;
        font-weight: 700;
        margin: 0 0 0 -10px;
    }

    .sectionContent {
        min-height: 10px;

        .bigSection {
            display: flex;
            flex-flow: row wrap;
            justify-content: flex-start;
            align-items: flex-start;
            overflow-y: scroll;
            min-height: 500px;
        }

        .smallSection {
            display: flex;
            flex-flow: row nowrap;
            justify-content: flex-start;
            align-items: center;
            overflow-x: scroll;
            min-height: 100px;
        }
    }

    
}

</style>

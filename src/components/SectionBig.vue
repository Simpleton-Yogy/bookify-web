<template>
    <div class="sectionContainer">
        <div class="sectionTitle">{{ title }}</div>
        <div class="sectionContent">
            <slot></slot>
        </div>
    </div>
</template>

<script>


export default {
  name: 'SectionBig',
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
    padding: 20px 0 20px 20px;
    background-color: $dark;
    border-radius: 10px 0 0 10px;
    margin-bottom: 5%;

    .sectionTitle {
        color: $text;
        font-family: 'Montserrat', sans-serif;
        font-size: 35px;
        font-weight: 700;
        margin: 0 0 15px -10px;
    }

    .sectionContent {
        display: flex;
        flex-flow: row wrap;
        justify-content: flex-start;
        align-items: flex-start;
        overflow-y: auto;
        min-height: 500px;
        width: 100%;
    }

    
}

</style>

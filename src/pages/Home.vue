<template>
    <div class="homeMainContainer">
    <SectionSmall title="Latest in your library"></SectionSmall>
    <SectionSmall title="Wanted books"></SectionSmall>
    <SectionSmall title="Most read this week"></SectionSmall>
  </div>
</template>

<script>

// Import Components
import SectionSmall from '@/components/SectionSmall.vue';


export default {
  name: 'App',
  components: {
    SectionSmall
    },
}
</script>

<style scoped lang="scss">

@import "@/assets/colors.scss";

.homeMainContainer {
    display: flex;
    flex-flow: column nowrap;
    width: 95%;
    padding-top: 5%;
}


</style>

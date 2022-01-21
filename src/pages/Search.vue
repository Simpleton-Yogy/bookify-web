<template>
    <div class="searchMainContainer">
        <div class="searchBarContainer">
            <div class="searchBarIcon" />
            <div class="searchBarInput" />
        </div>
        <SectionBig>

        </SectionBig>
    </div>
</template>

<script>

import SectionBig from '@/components/SectionBig.vue';

export default {
  name: 'Search',
  components: {
      SectionBig
  },
  data: function() {
    return {
    }
  },
}

</script>

<style scoped lang="scss">

@import "@/assets/colors.scss";

.searchMainContainer {
    display: flex;
    flex-flow: column nowrap;
    width: 95%;
    padding-top: 5%;
    margin-bottom: -100%;

    .searchBarContainer {
        display: flex;
        flex-flow: row nowrap;
        justify-content: flex-start;
        align-items: center;
        padding: 5px 0 5px 10px;
        border-radius: 10px 0 0 10px;
    }
}

</style>

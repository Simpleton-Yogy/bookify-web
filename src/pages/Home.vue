<template>
    <div class="homeMainContainer">
    <SectionSmall title="Latest in your library"><Book title="Test Book" author="b1u3-22" rating="5" release="2022" image="https://i.gr-assets.com/images/S/compressed.photo.goodreads.com/books/1555447414l/44767458.jpg" /></SectionSmall>
    <SectionSmall title="Wanted books"></SectionSmall>
    <SectionSmall title="Most read this week"></SectionSmall>
  </div>
</template>

<script>

// Import Components
import SectionSmall from '@/components/SectionSmall.vue';
import Book from '@/components/Book.vue';


export default {
  name: 'Home',
  components: {
    SectionSmall, Book
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

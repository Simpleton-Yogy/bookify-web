<template>
    <div class="homeMainContainer">
      <SectionSmall title="Latest in your library">
        <Book title="Test Book" author="b1u3-22" rating="5" release="2022" image="https://i.gr-assets.com/images/S/compressed.photo.goodreads.com/books/1555447414l/44767458.jpg" />
      </SectionSmall>
      <SectionSmall title="Wanted books"></SectionSmall>
      <SectionSmall title="Most read this week">
        <SectionLoader v-if="popularBooks.length < 1" text="Crunching the data" />
        <transition-group name="fade">
          <template v-for="book in popularBooks" :key="book.key">
              <Book :id="book.id" :title="book.title" :author="book.author" :release="book.release" :image="book.image" :status="book.status" />
          </template>
        </transition-group>
      </SectionSmall>
  </div>
</template>

<script>

// Import Components
import SectionSmall from '@/components/SectionSmall.vue';
import Book from '@/components/Book.vue';
import axios from 'axios';
import uniqueId from 'lodash.uniqueid';
import SectionLoader from '@/components/SectionLoader.vue';

export default {
  name: 'Home',
  components: {
    SectionSmall, Book, SectionLoader
  },
  data: function() {
    return {
      latestInLibraryBooks: [],
      wantedBooks: [],
      popularBooks: [],
    }
  },
  mounted: function() {
    axios
      .get('/getPopular')
      .then((response) => {
        for (const [key, value] of Object.entries(response.data)){
          this.popularBooks.push({
            'key': uniqueId('book-'),
            'id': value.id,
            'title': key,
            'author': value.author,
            'release': value.release,
            'image': value.image,
            'status': value.status
          })
        }
      })
  }
}

</script>

<style scoped lang="scss">

@import "@/assets/colors.scss";

.homeMainContainer {
    display: flex;
    flex-flow: column nowrap;
    width: 95%;
    padding-top: 5%;
    margin-bottom: -100%;
}

</style>
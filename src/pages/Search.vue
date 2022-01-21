<template>
    <div class="searchMainContainer">
        <div class="searchBarContainer">
            <img class="searchBarIcon" :src="require('../assets/magIcon.svg')" @click="searchOnEnter" />
            <input class="searchBarInput" placeholder="Go on, search for something!" v-model="queryInput" @input="onSearchChange" @keyup.enter="searchOnEnter"/>
        </div>
        <SectionBig title="Search results">
            <SectionLoader v-if="processing" :text="loaderTitle" />
            <div v-else-if="searchResults.length < 1" class="searchEmptyContainer">
                <div class="searchEmptyTitle">No results</div>
                <img class="searchEmptyIcon" :src="require('../assets/folderIcon.svg')" />
            </div>
            <transition-group name="fade">
                <template v-for="book in searchResults" :key="book.key">
                    <Book :title="book.title" :author="book.author" :release="book.release" :image="book.image" />
                </template>
            </transition-group>
        </SectionBig>
    </div>
</template>

<script>

import SectionBig from '@/components/SectionBig.vue';
import axios from 'axios';
import uniqueId from 'lodash.uniqueid';
import Book from '@/components/Book.vue';
import SectionLoader from '@/components/SectionLoader.vue';

export default {
  name: 'Search',
  components: {
      SectionBig, Book, SectionLoader
  },
  data: function() {
    return {
        searchTimeout: null,
        searchResults: [],
        queryInput: "",
        processing: false,
        loaderTitle: ""
    }
  },
  methods: {
      onSearchChange: function() {
          if (this.searchTimeout) {
              clearTimeout(this.searchTimeout)
          }

        if (this.queryInput === ""){
            this.processing = false;
            this.searchResults = []
        }
        else{
            this.searchResults = []
            this.loaderTitle = "Processing"
            this.processing = true
        }

        this.searchTimeout = setTimeout(() => {
            this.searchBooks(this.queryInput)
            
            }, 500)
      },

      searchOnEnter: function() {
          if (this.searchTimeout) {
              clearTimeout(this.searchTimeout)
          }

          this.searchBooks(this.queryInput)
      },

      searchBooks: function(queryInput) {

          this.loaderTitle = "Searching"

          axios
            .post("/search", {query: queryInput})
            .then((response) => {

                this.processing = false
                this.searchResults = []

                for (const [key, value] of Object.entries(response.data)){
                    this.searchResults.push({
                        'key': uniqueId('book-'),
                        'title': key,
                        'author': value.author,
                        'release': value.release,
                        'image': value.image
                    })
                    }
            })
      }
  }
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
        padding: 10px 0 10px 10px;
        border-radius: 10px 0 0 10px;
        width: 100%;
        background-color: $dark;
        margin-bottom: 5%;

        .searchBarIcon {
            height: 24px;
            width: auto;
            margin: -2px 20px -2px 10px;
            cursor: pointer;
        }

        .searchBarInput {
            width: 100%;
            border: none;
            background-color: $dark;
            color: $text;
            font-family: 'Montserrat', sans-serif;
            font-size: 24px;
            font-weight: 500;

            &:focus {
                outline: none;
            }
        }
    }

    .searchEmptyContainer {
        width: 100%;
        height: 100%;
        display: flex;
        flex-flow: column nowrap;
        align-items: center;
        justify-content: center;

        .searchEmptyTitle {
            color: $text;
            font-family: 'Montserrat', sans-serif;
            font-style: normal;
            font-weight: bold;
            font-size: 35px;
            margin-bottom: 15px;
        }
    }
}

</style>

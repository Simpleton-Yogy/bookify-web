<template>
    <div class="bookDetailsMainContainer">
        <transition name="slide-fade-nd">
        <div v-if="loaded" class="bookDetailsTopContainer">
            <div class="bookDetailsImageContainer">
                <img class="bookDetailsImage" :src="image" />
            </div>
            <div class="bookDetailsTextMainContainer">
                <div class="bookDetailsTextLeftContainer">
                    <div class="bookDetailsTitle">{{ title }}</div>
                    <div class="bookDetailsAuthor">{{ author }}</div>
                    <div class="bookDetailsMiscContainer">
                        <div v-if="pages" class="bookDetailsMisc">📝 {{ pages }} Pages</div>
                        <div v-if="rating" class="bookDetailsMisc">🔥 {{ rating }} Rating</div>
                        <div v-if="release" class="bookDetailsMisc">🕒 Released in {{ release }}</div>
                    </div>
                </div>
                <div class="bookDetailsTextSeparator" />
                <div class="bookDetailsTextRightContainer">
                    <div class="bookDetailsTextDescription">{{ description }}</div>
                </div>
            </div>
        </div>
        </transition>
        <div v-if="!loaded" class="bookDetailsLoaderContainer">
            <SectionLoader :text="loaderText" />
        </div>
    </div>
</template>

<script>


import axios from 'axios';
import SectionLoader from '@/components/SectionLoader.vue';

export default {
    name: 'Search',
    components: {
        SectionLoader
    },
    props: [
        'bookID'
    ],
    data: function () {
        return {
            loaded: false,
            loaderText: "Finding the right page"
        }
    },
    mounted: function() {
      axios
        .post("/getBookInfo", {book_id: this.bookID})
        .then(response => {
            this.title = response.data["title"]
            this.author = response.data["author"]
            this.pages = response.data["pages"]
            this.release = response.data["release"]
            this.rating = response.data["rating"]
            this.image = response.data["image"]
            this.description = response.data["description"]
            this.loaded = true
        })
    }
}

</script>

<style scoped lang="scss">

@import "@/assets/colors.scss";

.bookDetailsMainContainer {
    display: flex;
    flex-flow: column nowrap;
    width: 95%;
    padding-top: 5%;
    margin-bottom: -100%;
    height: 95%;

    .bookDetailsTopContainer {
        display: flex;
        flex-flow: row nowrap;
        justify-content: flex-start;
        align-items: flex-start;
        width: 100%;

        .bookDetailsImageContainer {
            display: flex;
            flex-flow: column nowrap;
            align-items: center;
            justify-content: center;
            margin: -6% 5% 0 0;
            padding: 0 1% 1% 1%;
            background-color: $dark;
            border-radius: 0 0 10px 10px;

            .bookDetailsImage {
                border-radius: 0 0 10px 10px;
            }
        }

        .bookDetailsTextMainContainer {
            display: flex;
            flex-flow: row nowrap;
            align-items: stretch;
            justify-content: center;
            background-color: $dark;
            border-radius: 10px;
            padding: 2%;
            width: 100%;

            .bookDetailsTextLeftContainer {
                display: flex;
                flex-flow: column nowrap;
                justify-content: flex-start;
                align-items: center;
                font-family: 'Montserrat' sans-serif;
                font-style: normal;
                color: $text;
                width: 48%;

                .bookDetailsTitle {
                    font-weight: 600;
                    font-size: 35px;
                    width: 100%;
                    margin: 0;
                }

                .bookDetailsAuthor {
                    font-weight: 500;
                    font-size: 22px;
                    width: 100%;
                    margin: 2% 0 3% 0;
                }

                .bookDetailsMiscContainer {
                    display: flex;
                    flex-flow: row nowrap;
                    justify-content: space-between;
                    align-items: center;
                    width: 100%;
                    margin: 3% 0;

                    .bookDetailsMisc {
                        font-weight: 400;
                        font-size: 16px;
                    }
                }
            }

            .bookDetailsTextSeparator {
                width: 8px;
                border-radius: 2px;
                background-color: $light;
                margin: 0 3%;
            }

            .bookDetailsTextRightContainer {
                display: flex;
                flex-flow: column nowrap;
                justify-content: center;
                align-items: flex-start;
                width: 48%;

                .bookDetailsTextDescription {
                    font-weight: 200;
                    font-size: 16px;
                }
            }
        }
    }

    .bookDetailsLoaderContainer {
        display: flex;
        flex-flow: column nowrap;
        align-items: center;
        justify-content: center;
        height: 100%;
        width: 100%;
    }
}

</style>

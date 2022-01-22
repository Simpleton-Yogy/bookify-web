<template>
    <div class="bookContainer">
        <div class="bookImageStack">
            <div v-if="status" class="bookStatusLabel" :class="{ redStatusLabel: status === 'Missing' || status === 'Dowloading', greenStatusLabel: status === 'Available' || status === 'Gathering' }" >{{ status }}</div>
            <img class="bookImage" :src="image" loading="lazy"/>
            <div class="bookSeeDetails" @click="requestBookPage">See details</div>
        </div>
        <div class="bookTextContainer">
            <div class="bookTitle">{{ title.replace(/: .*/gm, "") }}</div>
            <div class="bookAuthor">{{ author }}</div>
            <div class="bookRating">{{ rating }}</div>
            <div class="bookRelease">{{ release }}</div>
            <div class="bookButtonsContainer">
                <Button>Request</Button>
            </div>
        </div>
    </div>
</template>

<script>

import Button from '@/components/Button.vue';

export default {
  name: 'Book',
  components: {
    Button
  },
  props: [
      'title', 'author', 'image', 'rating', 'release', 'status', 'id'
  ],

  methods: {
      requestBookPage: function() {
        this.emitter.emit('request-book-page', this.id)
      },

      requestBook: function() {

      },

      getBookStatus: function() {

      }
  },

  data: function () {
      return {
          
      }
  }
}


</script>

<style scoped lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,100;1,200;1,300;1,400;1,500;1,600;1,700&display=swap');
@import "@/assets/colors.scss";

.bookContainer {
    min-width: 320px;
    max-width: 320px;
    display: flex;
    flex-flow: row nowrap;
    align-items: stretch;
    justify-content: space-between;
    padding: 5px;
    border-radius: 5px;
    background-color: $light;
    margin: 0 10px 20px 10px;

    .bookImageStack {
        display: flex;
        flex-flow: column nowrap;
        justify-content: center;
        align-items: center;
        font-size: 12px;
        font-weight: 600;
        color: $text;

        .bookStatusLabel {
            color: $text;
            text-align: center;
            height: 24px;
            margin: 0 0 -24px 0;
            z-index: 1;
            background-color: $blue;
            border-radius: 5px;
            width: 100%;
            padding: 0;
            display: flex;
            flex-flow: column nowrap;
            align-items: center;
            justify-content: center;
        }   

        .bookImage {
            height: 193px;
            width: auto;
            border-radius: 5px;
            z-index: 0;
            margin: 0;
        }

        .bookSeeDetails{
            color: $text;
            text-align: center;
            height: 24px;
            margin: -24px 0 0 0;
            z-index: 2;
            background-color: $blue;
            border-radius: 5px;
            width: 100%;
            padding: 0;
            display: flex;
            flex-flow: column nowrap;
            align-items: center;
            justify-content: center;
            transition: all 220ms ease-in-out;
            cursor: pointer;

            &:hover {
                height: 193px;
                margin: -193px 0 0 0;
                animation: seeDetailsAnimation;
                animation-duration: 220ms;
                animation-timing-function: ease-in-out;
                filter: brightness(120%);
            }
        }
    }

    .bookTextContainer {
        display: flex;
        flex-flow: column nowrap;
        align-items: center;
        justify-content: flex-start;
        margin-left: 5px;
        color: $text;
        font-family: 'Montserrat', sans-serif;
        text-align: center;
        width: 100%;

        .bookTitle {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 10px;
        }

        .bookAuthor {
            font-size: 12px;
            font-weight: 600;
            margin-bottom: 10px;
        }

        .bookRating {
            font-size: 10px;
            font-weight: 300;
            margin-bottom: 10px;
        }

        .bookRelease {
            font-size: 10px;
            font-weight: 500;
        }

        .bookButtonsContainer {
            margin-top: auto;
            width: 80%;
            display: flex;
            flex-flow: row nowrap;
            justify-content: center;
            align-items: center;
        }
    }
}

@keyframes seeDetailsAnimation {
    0% {
        border-radius: 5px;
    }
    50% {
        border-radius: 50% 50% 5px 5px;
    }
    100% {
        border-radius: 5px;
    }
}


</style>

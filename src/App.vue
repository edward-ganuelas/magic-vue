<template>
  <div id="app">
    <cards v-bind:cards="cards"></cards>
  </div>
</template>

<script>
import { MAGICAPI } from "./js/constants.js";
import Cards from "./components/Cards";
import axios from "axios";
export default {
  name: "app",
  components: { Cards },
  data() {
    return {
      cards: "",
      page: 1
    };
  },
  methods: {
    getCards: function() {
      const URL = MAGICAPI.cards + "?page=" + this.page;
      if (sessionStorage.getItem(URL) === null) {
        axios
          .get(URL)
          .then(x => {
            this.cards = x.data.cards;
            // this.page++;
            sessionStorage.setItem("cardPage", this.page);
            sessionStorage.setItem(URL, JSON.stringify(x.data.cards));
          })
          .catch(x => console.log(x));
      }else{
        this.cards = JSON.parse(sessionStorage.getItem(URL));
      }
    }
  },
  beforeMount: function() {
    if (sessionStorage.getItem("cardPage") === null) {
      sessionStorage.setItem("cardPage", this.page);
    } else {
      this.page = sessionStorage.getItem("cardPage");
    }
    this.getCards();
  }
};
</script>

<style lang="scss">

</style>

<template>
  <div id="app">
    <a v-on:click="prev" v-if="headerLinks.prev !==undefined">Prev</a>
    <a v-on:click="next">Next</a>
    <cards v-bind:cards="cards"></cards>
    
  </div>
</template>

<script>
import { MAGICAPI } from "./js/constants.js";
import Cards from "./components/Cards";
import axios from "axios";
var parse = require("parse-link-header");
export default {
  name: "app",
  components: { Cards },
  data() {
    return {
      cards: "",
      headerLinks: ""
    };
  },
  methods: {
    getCards: function() {
      const URL = MAGICAPI.cards;
      if (sessionStorage.getItem(URL) === null) {
        axios
          .get(URL)
          .then(x => {
            this.cards = x.data.cards;
            this.headerLinks = parse(x.headers.link);
            // this.page++;

            sessionStorage.setItem(URL, JSON.stringify(x.data.cards));
          })
          .catch(x => console.log(x));
      } else {
        this.cards = JSON.parse(sessionStorage.getItem(URL));
      }
    },
    next: function() {

      if (sessionStorage.getItem(this.headerLinks.next.url) === null) {
        axios
          .get(this.headerLinks.next.url)
          .then(x => {
            this.cards = x.data.cards;
            sessionStorage.setItem(
              this.headerLinks.next.url,
              JSON.stringify(x.data.cards)
            );
            this.headerLinks = parse(x.headers.link);
            // this.page++;


          })
          .catch(x => console.log(x));
      } else {
        this.cards = JSON.parse(
          sessionStorage.getItem(this.headerLinks.next.url)
        );
      }
    },
    prev: function() {
      if (sessionStorage.getItem(this.headerLinks.prev.url) === null) {
        axios
          .get(this.headerLinks.prev.url)
          .then(x => {
            this.cards = x.data.cards;
            sessionStorage.setItem(
              this.headerLinks.prev.url,
              JSON.stringify(x.data.cards)
            );
            this.headerLinks = parse(x.headers.link);
            // this.page++;

          })
          .catch(x => console.log(x));
      } else {
        this.cards = JSON.parse(
          sessionStorage.getItem(this.headerLinks.prev.url)
        );
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

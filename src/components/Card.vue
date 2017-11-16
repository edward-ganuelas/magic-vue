<template>
  <div class="card">
      <img v-bind:src="cardItem.imageUrl" v-bind:alt="cardItem.name" v-on:click="showDetails" />
      <div class="details" v-show="detailsHide == true">
          <p>Name: {{cardItem.name}}</p>
          <p>Rarity: {{cardItem.rarity}}</p>
          <p>{{cardItem.text}}</p>
      </div>
  </div>
</template>

<script>
export default {
  name: "card",
  props: ["cardItem"],
  data() {
    return {
      detailsHide: false
    };
  },
  methods: {
    showDetails: function() {
      this.detailsHide = this.detailsHide == true ? false : true;
    }
  }
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.card {
  margin-right: 5px;
  margin-bottom: 10px;
  padding: 5px;
}
</style>

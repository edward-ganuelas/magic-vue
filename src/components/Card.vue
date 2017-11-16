<template>
  <div class="card">
      <img v-bind:src="cardItem.imageUrl" v-bind:alt="cardItem.name" />
  </div>
</template>

<script>
export default {
  name: "card",
  props: ["cardItem"],
  data() {
    return {};
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.card {
  margin-right: 5px;
  margin-bottom: 10px;
  border-radius: 15px;
  border: solid 1px #000;
  padding: 5px;
}
</style>

<template>
  <div class="cards">
    <div class="card" v-for="card in cards" v-bind:key="card.id">
        <h3>{{card.name}}</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Cards',
  props: ['cards'],
  data () {
    return {

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.cards{
    display: flex;
    flex-wrap: wrap;
    .card{
        margin-right: 5px;
    }
}

</style>

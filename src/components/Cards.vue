<template>
  <div class="cards">
    <div class="card" v-for="item in cards" v-bind:key="item.id">
        <card v-bind:cardItem="item"></card>
    </div>
  </div>
</template>

<script>
import Card from './Card';

export default {
  name: 'Cards',
  components: {
      Card
  },
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

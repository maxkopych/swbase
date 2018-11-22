<template>
  <div id="app">
  <h1 class="text-center my-5">Generate Your Team</h1>
    <div v-if="!characters.length">
      <h3 class="text-center">Loading...</h3>
    </div>
    <div v-else>
      <div v-for="(character, index) in characters" class="col-xs-12 col-sm-6 col-md-4">
        <Character :info="{character,index}"></Character>
      </div>
    </div>
  </div>
</template>

<script>
  import Character from "./components/Character"
export default {
  name: 'app',
  components:{
    Character
  },
  data () {
    return {
      characters: []
    }
  }
}
</script>

<style lang="scss">

</style>

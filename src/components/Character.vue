<template>
  <div class="card" @click="changeCharacter">
    <h3 class="card-title text-center text-warning">{{info.character.name}}</h3>
    <ul class="list-group">
      <li class="list-group-item">height: {{info.character.height}}</li>
      <li class="list-group-item">mass: {{info.character.mass}}</li>
      <li class="list-group-item">hair_color: {{info.character.hair_color}}</li>
      <li class="list-group-item">skin_color: {{info.character.skin_color}}</li>
      <li class="list-group-item">gender: {{info.character.gender}}</li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: "Character",
    props: [
      "info"
    ],
    methods:{
      changeCharacter(){
        this.$root.$emit("changeSingleCharacter",this.info.index);
      }
    }
  }
</script>

<style scoped>
.card{
  cursor: pointer;
  
}
</style>
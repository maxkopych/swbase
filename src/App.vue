<template>
  <div id="app" class="container">
  <h1 class="text-center my-5">Generate Your Team</h1>
    <div v-if="!characters.length">
      <h3 class="text-center">Loading...</h3>
    </div>
    <div v-else class="row">
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
      characters: [],
      total: 0,
    }
  },
  created(){
    fetch("https://swapi.co/api/people/",{method:"GET"}).then( res=>res.json()).then( json => { //fetch сперва привотит все хеды а потом тело
      this.total=json.count;
      
    })
      .catch(error=>console.log(error));
    
    //########################################
    this.$root.$on("changeSingleCharacter",(val)=>{
      let $rand = Math.floor(Math.random() * this.total) + 1;
      while(this.characters.find(el=>{
        return el.index == $rand //??
      })){
        $rand = Math.floor(Math.random() * this.total) + 1;
      }
      fetch("https://swapi.co/api/people/" + $rand ).then( res=>res.json()).then( json => {
        json.index= $rand;
        this.$set(this.characters,val,json)
      })
        .catch(error=>console.log(error));
    })
    //########################################
  },
  watch:{
    total: function(val) { //Can't use Arrow Functions for watches
      let i=0;
      let $rand
      while(i<3 ){
        $rand = Math.floor(Math.random() * val) + 1;
        if(this.characters.find(el=>{
         return el.index == $rand
        })){
          continue;
        }
        i++;
        fetch("https://swapi.co/api/people/" + $rand ).then( res=>res.json()).then( json => {
          json.index= $rand
          this.characters.push(json);
          //
        })
          .catch(error=>console.log(error));
      }
    }
  }
}
</script>

<style lang="scss">

</style>

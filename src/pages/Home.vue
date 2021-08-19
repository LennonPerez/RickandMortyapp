<template>
  <header>
      <div class="dark-bg"/>
          <div class="logo" />
         <div class="input-box">
           <input type="text" placeholder="Busca un personaje" v-model="name"/>
         <i class="fas fa-search"></i>
      </div>
  </header>
  <Navbar @gender="getGender"/>
  <main>
    <!-- <p class="favorites">Mostrar favoritos <span ><i class="fas fa-star"></i></span></p> -->
    <CharactersList :filtername="name" :filtergender="filtergender"/>
  </main>
  <footer>
    <div class="dark-bg"/>
    <div class="logo" />
  </footer>
</template>

<script>
import {defineAsyncComponent} from "vue"
export default {
    components : {
        Navbar : defineAsyncComponent(()=> import("@/components/Navbar")),
        CharactersList : defineAsyncComponent(()=> import("@/components/CharactersList"))
    },
    data(){
      return{
        name : null,
        filtergender : null
      }
    },
    methods : {
      getGender(msg){
        this.filtergender = msg === "all" ? null : msg
      }
    }
}
</script>

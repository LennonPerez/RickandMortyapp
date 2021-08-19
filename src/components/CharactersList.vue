<template>
    <div class="characters-list-container">
        <template v-for="character in filtername ? filteredByName : filteredByGender" :key="character.id" >
        <Character :character="character" @click="selectCharacter(character)" />
        </template>
    </div>
    <div class="page-manager">
        <button type="button" @click="managePages" :disabled="actualpage === 1" >Previous page</button>
        <button type="button" @click="managePages" :disabled="actualpage === 34">Next page</button>
    </div>
    <Modal 
    v-if="selectedCharacter" 
    :character="selectedCharacter" 
    :characters="characters"
    @select="selectCharacter"
    @exit="selectCharacter"
    />
</template>

<script>
import {defineAsyncComponent} from "vue"
export default {
    components : {
        Character : defineAsyncComponent(()=> import("@/components/Character")),
        Modal : defineAsyncComponent(()=> import("@/components/Modal")),
    },
    data(){
        return{
            characters : null,
            selectedCharacter : null,
            actualpage : 1
        }
    },
    props : 
      ["filtername", "filtergender"]  
    ,
    methods : {
        async getCharacters(){
            const url =`https://rickandmortyapi.com/api/character/?page=${this.actualpage}`
            const {results} = await fetch(url).then(r => r.json())
            this.characters = results
        },
        selectCharacter(character){
            this.selectedCharacter = character
        },
        managePages(e){
            if(e.target.textContent === "Next page"){
                this.actualpage++
            }else{
                this.actualpage--
            }
            window.scroll(0, 0)
            this.getCharacters()
        },
    },
    computed : {
        filteredByName(){
            return this.filtername 
            ? this.characters.filter(char => char.name.toLowerCase().includes(this.filtername)) 
            : null
        },
        filteredByGender(){
            return this.filtergender
            ? this.characters.filter(char => char.gender === this.filtergender)
            : this.characters
        }
    },
    created(){
        this.getCharacters()
    }
}
</script>
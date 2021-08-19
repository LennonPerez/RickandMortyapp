<template>
    <div class="dark-bg dark-bg-modal"/>
    <div class="modal-container">
        <div class="cover-background">
            <i class="fas fa-times-circle" @click="$emit('exit', null)"></i>
            <!-- <p class="favorites"><span><i class="fas fa-star"></i></span></p> -->
        <img :src="character.image" :alt="character.name" class="character-picture" />
        </div>
        <div class="character-name-status">
            <p>{{character.status}}</p>
            <h2>{{character.name}}</h2>
            <p>{{character.species}}</p>
        </div>
        <div class="info-container">
        <h2 class="info-title">Information</h2>
        <div class="aditional-info">
            <div class="gender-box box">
                <p>gender</p>
                <h3>{{character.gender}}</h3>
            </div>
            <div class="origin-box box">
                <p>origin</p>
                <h3>{{character.origin.name}}</h3>
            </div>
            <div class="type-box box">
                <p>type</p>
                <h3>{{getCharacterType}}</h3>
            </div>
        </div>
        <h2 class="info-title">Episodes</h2>
        <div class="episodes-list">
            <template v-for="episode in episodes" :key="episode.id">
            <Episode :episode="episode" />
            </template>
        </div>
        <h2 class="info-title">Interesting characters</h2>
        <div class="interesting-characters">
            <template v-for="character in getNewArray" :key="character.id">
            <Character :character="character" @click="$emit('select', character)"/>
            </template>
        </div>
        </div>
    </div>
</template>

<script>
import { defineAsyncComponent } from 'vue'
export default {
    components : {
        Episode : defineAsyncComponent(()=>import("@/components/Episode")),
        Character : defineAsyncComponent(()=>import("@/components/Character"))
    },
     props : {
         character : {
             type : Object,
             required : true
         },
         characters : {
             type : Array,
             required : true
         }
     },
     data(){
         return{
             episodes : []
         }
     },
     emits : ["select", "exit"],
    computed : {
        getCharacterType(){
            return this.character.type ? this.character.type : "Unknown"
        },
        getNewArray(){
            return this.characters.filter(char => char.id !== this.character.id).reverse()
        }
    },
    methods : {
        getEpisodes(){
            this.character.episode.map(async ep => this.episodes.push(await fetch(ep).then(r => r.json())))
        }
    }, created(){
        this.getEpisodes()
    }
}
</script>
<template>
    <div class="Character">
        <img :src="char.image" :alt="char.name + ' image'">
        <div class="character-info">
            <p :class="char.status">{{char.status}}-{{char.species}}</p>
            <h2>{{char.name}}</h2>
            <p>last known location</p>
            <h4>{{char.location.name}}</h4>
            <p>first seen in</p>
            <h3>{{firstepisode}}</h3>
            <!-- <p class="favorites"><span><i class="fas fa-star"></i></span></p> -->
        </div>
    </div>
</template>

<script>
export default {
    props : {
        character : {
            type : Object,
            required : true
        },
    },
    data(){
        return{
            char : this.character,
            firstepisode : null
        }
    },
    methods : {
        async getFirstEpisode(){
            const res = await fetch(this.character.episode[0])
            const result = await res.json()
            this.firstepisode = result.name
        }
    },
    created(){
        this.getFirstEpisode()
    }
}
</script>
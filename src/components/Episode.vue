<template>
    <div class="episode-container">
        <p>{{episode.name}}</p>
        <h3>{{episode.episode}}</h3>
        <p>{{episode.air_date}}</p>
    </div>
</template>

<script>
export default {
    props : {
        episode : {
            type : Object,
            required : true
        }
    }
}
</script>
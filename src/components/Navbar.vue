<template>
    <nav>
        <ul class="desktop-nav">
            <li><button class="gender-button" @click="getGender">all</button></li>
            <li><button class="gender-button" @click="getGender">unknown</button></li>
            <li><button class="gender-button" @click="getGender">Male</button></li>
            <li><button class="gender-button" @click="getGender">Female</button></li>
            <li><button class="gender-button" @click="getGender">Genderless</button></li>
        </ul>
    </nav>
</template>

<script>
export default {
    emits : ["gender"],
    methods : {
        getGender(e){
            this.$emit('gender', e.target.textContent)
            const buttons = document.querySelectorAll(".gender-button")
            buttons.forEach(btn => {
                if(btn.classList[1] === "selectedbutton"){
                   btn.classList.remove("selectedbutton")
                }
            })
            e.target.classList.add("selectedbutton")
        }
    }
}
</script>
<template>
    <div>
        <div class="container">
            <img id="logo" src="../../assets/logo.png">
        </div>
        <div class="btn-group">
            <button class="btn draw-border" @click="goToPage('game')">Show Game</button>
            <button class="btn draw-border" @click="goToPage('ranking')">Show Ranking</button>
        </div>
        
    </div>
</template>

<script>
export default {
    name: "Homepage",
    methods: {
        goToPage(page) {
            this.$emit("change-page", page);
        }
    }
}
</script>
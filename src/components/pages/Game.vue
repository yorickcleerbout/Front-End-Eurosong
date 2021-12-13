<template>
    <div>
        <h1>Game</h1>
        <button @click="goToPage('home')">Go To Home</button>
    </div>
</template>

<script>
export default {
    name: "Gamepage",
    methods: {
        goToPage(page) {
            this.$emit("change-page", page);
        }
    }
}
</script>
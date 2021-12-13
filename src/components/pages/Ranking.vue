<template>
    <div>
        <h1>Ranking</h1>
      <button @click="goToPage('home')">Go To Home</button>
    </div>
</template>

<script>
export default {
    name: "Rankingpage",
    methods: {
        goToPage(page) {
            this.$emit("change-page", page);
        }
    }
}
</script>
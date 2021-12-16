<template>
    <div>
        <!--  Navigation -->
        <nav>
            <img src="../../assets/logoblack.png" width="150"/>
            <ul>
                <li @click="goToPage('home')">Home</li>
                <li @click="goToPage('game')">Voting Game</li>
                <li @click="goToPage('ranking')">Ranking</li>
            </ul>
        </nav>
        
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
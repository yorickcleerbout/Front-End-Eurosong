<template>
    <div class="container">
        <img src="../assets/arrowleft.png" @click="changeIndex(-1)" width="100">
        <div class="card">
            <div class="imgBx">
                <div v-for="(song, index) in items" :key="song.id" v-if="index == activeIndex">              
                    <iframe :src="song.spotify" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
                </div>
            </div>

            <div class="contentBx">

                <h2 v-for="(song, index) in items" :key="song.id" v-if="index == activeIndex">{{ song.title }}</h2>

                <div class="size">
                    <h3 v-for="(song, index) in items" :key="song.id" v-if="index == activeIndex">{{ song.artist.name }}</h3>
                </div>

                <div class="color">
                    <h3 v-for="(point, index) in points" :key="index" v-if="index == activeIndex">Current Points: {{points[index]}}</h3>
                </div>

            </div>
        </div>
        <img src="../assets/arrowright.png" @click="changeIndex(1)" width="100">
    </div>
</template>
<script>
export default {
    name: "VoteCard",
    props: [
        "items",
        "activeIndex",
        "points"
    ],
    methods: {
        changeIndex(value) {
            let index = this.activeIndex;

            index += value;
            if (index < 0) index = this.items.length -1;
            else if (index == this.items.length) index = 0;

            this.$emit('change-index', index);
        }
    }
}
</script>
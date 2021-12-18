<template>
    <div class="card">
        <div class="imgBx">                  
            <iframe :src="song.spotify" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
        </div>

        <div class="contentBx">
            <h2>{{ song.title }} - {{ song.artist.name }}</h2>
            <div class="size">
                <h3 v-if="position == 1">{{ position }}st place</h3>
                <h3 v-else-if="position == 2">{{ position }}nd place</h3>
                <h3 v-else-if="position == 3">{{ position }}rd place</h3>
            </div>

            <div class="color">
                <h3>Points: {{ song.points }}</h3>
            </div>

        </div>
    </div>
</template>
<style>

.card:after {
    content: "Rank";
    position: absolute;
    top: 30%;
    left: -5%;
    font-size: 9em;
    font-weight: 800;
    font-style: italic;
    color: rgba(255, 255, 255, 0.04);

}

.container .card:nth-child(odd) {
    transform: translateY(15%);
}

</style>
<script>
export default {
    name: "RankCard",
    props: [
        "song",
        "position"
    ]
}
</script>
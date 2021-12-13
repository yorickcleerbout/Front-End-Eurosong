<template>
    <div>
        <div v-for="song in items" :key="song.id">
            {{ song.artist.name }} - {{ song.title }}
        </div>
    </div>
</template>

<script>
export default {
    name: "Carousel",
    props: [
        "items"
    ]
}
</script>
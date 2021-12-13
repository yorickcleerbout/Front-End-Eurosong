<template>
    <div>
        <h1>Game</h1>
        <button @click="goToPage('home')">Go To Home</button>

        
        <Carousel :items="songs"/>
    </div>
</template>

<script>
// Components
import Carousel from '../Carousel.vue';

export default {
    name: "Gamepage",
    components: {
        Carousel
    },
    data() {
        return {
            songs: []
        }
    },
    mounted() {
        console.log("Mounted and ready to fetch data!");
        this.fetchSongs();
        
        

    },
    methods: {
        // Navigation
        goToPage(page) {
            this.$emit("change-page", page);
        },
        // Data Methods
        fetchSongs() {
            const url = "http://webservies.be/eurosong/Songs";
            fetch(url)
                .then((response) => {
                    return response.json();
                })
                .then((songs) => {
                    this.fetchArtists(songs);
                });
        },
        fetchArtists(songs) {
            const url = "http://webservies.be/eurosong/Artists";
            fetch(url)
                .then((response) => {
                    return response.json();
                })
                .then((artists) => {
                    songs.map(song => {
                       const artist = artists.find((artist) => artist.id == song.artist);
                       song.artist = artist;
                       return song;
                    });
                    this.songs = songs;
                });
        }


    }
}
</script>
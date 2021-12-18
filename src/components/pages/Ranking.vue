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
        <div class="center">
            <h1><u>Ranking</u></h1>
            <div class="container" style="display:flex; justify-content:space-between">
                <RankCard :song="songs[1]" :position="2"/>
                <RankCard :song="songs[0]" :position="1"/>
                <RankCard :song="songs[2]" :position="3"/>
            </div>
            

        </div>
    </div>
</template>
<style>
.center {
    width: 50%;
}

</style>
<script>
import RankCard from '../RankCard.vue';

export default {
    name: "Rankingpage",
    components: {
        RankCard

    },
    data() {
        return {
            songs: []
        }
    },
    methods: {
        goToPage(page) {
            this.$emit("change-page", page);
        },
        fetchSongs() {
            const url = "http://webservies.be/eurosong/Songs";
            fetch(url)
                .then((response) => {
                    return response.json();
                })
                .then((songs) => {
                    let correctSongs = songs.filter(song => song.spotify != "string");
                    this.fetchVotes(correctSongs);
                    this.fetchArtists(correctSongs);
                    
                });
        },
        fetchVotes(songs) {
            const url = "http://webservies.be/eurosong/Votes";
            fetch(url)
                .then((response) => {
                    return response.json();
                })
                .then((votes) => {
                    songs.map(song => {
                       const vote = votes.filter((vote) => vote.songID == song.id);
                       song.points = 0;
                       vote.forEach(v => {
                           if (v.songID == song.id) song.points += v.points
                       });
                       return song;
                    });
                    let sorted = songs.sort((a, b) => (a.points < b.points ? 1 : -1));
                    this.songs = sorted;   
                    
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
    },
    mounted() {
        this.fetchSongs();
    }
}
</script>
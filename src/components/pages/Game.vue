<template>
    <div>
        <!--  Navigation -->
        <nav>
            <img src="../../assets/logoblack.png" width="150"/>
            <ul>
                <li @click="goToPage('home')">Home</li>
                <li @click="goToPage('ranking')">Ranking</li>
            </ul>
        </nav>
        
        <h1>Game</h1>
        
        <!-- Carousel -->
        <Carousel :items="songs" :activeIndex="activeSongIndex" @change-index="changeActiveSongIndex" />

        <div v-for="(vote, index) in votes" :key="index">
            <button v-if="!vote.isVoted"  @click="addVote(vote.points)">
                Add {{ vote.points }} points
            </button>
        </div>
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
            songs: [],
            activeSongIndex: 0,
            votes: [
                {
                    points: 1,
                    isVoted: false
                },
                {
                    points: 2,
                    isVoted: false
                },
                {
                    points: 4,
                    isVoted: false
                },
                {
                    points: 8,
                    isVoted: false
                },
                
            ]
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
        },

        postVote(points) {
            const songID = this.songs[this.activeSongIndex].id;
            const url = "http://webservies.be/eurosong/Votes";
            // ip grabber https://api.ipify.org/?format=jsonp&callback=getIP
            fetch(url, {
                method: "POST",
                headers: {
                    'Accept': 'application/json, text/plain',
                    'Content-Type': 'application/json;charset=UTF-8'
                },
                body: JSON.stringify({
                    songID: songID,
                    points: points
                })
            })
            .then((response) => {
                return response.json();
            })
            .then((result) => {
                console.log(result);
            });
        },

        // Logic Methods
        changeActiveSongIndex(index) {
            this.activeSongIndex = index;
        },

        addVote(points) {
            let votes = this.votes;

            votes.map((vote) => {
                if(vote.points == points) vote.isVoted = true;
                return vote;
            });
            
            this.postVote(points);

            let activeVotes = votes.filter((vote) => vote.isVoted == true);
            
            if (activeVotes.length == votes.length) this.goToPage("ranking");
        }


    }
}
</script>
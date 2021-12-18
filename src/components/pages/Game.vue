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
            <h1><u>Voting Game</u></h1>

            <!-- VoteCard -->
            <VoteCard :items="songs" :points="songPoints" :activeIndex="activeSongIndex" @change-index="changeActiveSongIndex" />
           
            
            <div class="btn-group">
                <div v-for="(vote, index) in votes" :key="index">
                    <button class="btn draw-border" v-if="!vote.isVoted"  @click="addVote(vote.points)">
                        Add {{ vote.points }} points
                    </button>
                </div>
            </div>
            <Feedback :message="note.msg" :classType="note.classType" /> 
        
        </div>
    </div>
</template>

<script>
// Components
import Feedback from '../Feedback.vue';
import VoteCard from '../VoteCard.vue';

export default {
    name: "Gamepage",
    components: {
        Feedback,
        VoteCard
    },
    data() {
        return {
            note: {
                msg: "Note: You can only use each amount of points once.",
                classType: "warning"
            },
            songs: [],
            songPoints: [],
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
                
            ],
            ip: null
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
                    let correctSongs = songs.filter(song => song.spotify != "string");
                    this.fetchArtists(correctSongs);
                    let songIDS = [];
                    correctSongs.forEach(song => {
                        songIDS.push(song.id);
                    });
                    this.fetchSongPoints(songIDS);
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

            // IP Grabber
            fetch('https://api.ipify.org?format=json')
                .then(x => x.json())
                .then(({ ip }) => {
                    this.ip = ip;
                    fetch(url, {
                        method: "POST",
                        headers: {
                            'Accept': 'application/json, text/plain',
                            'Content-Type': 'application/json;charset=UTF-8'
                        },
                        body: JSON.stringify({
                            songID: songID,
                            points: points,
                            ip: this.ip
                        })
                    })
                    .then((response) => {
                        return response.json();
                    })
                    .then((result) => {
                        
                    });
            });

            
            
        },

        fetchSongPoints(songIDS) {
            songIDS.forEach(id => {
              fetch(`http://webservies.be/eurosong/Songs/${id}/points`)
                .then((response) => {
                        return response.json();
                })
                .then((points) => { 
                    this.songPoints.push(points);
                });
                       
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
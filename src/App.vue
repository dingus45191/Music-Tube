<template>
<div id="app">
    <header>
        <h1 >My Music </h1>
    </header>
<main>
<section class="player">
<h2 class="song-title">
{{current.title}} - <span>{{current.artist }}</span>
</h2>
<div class="controls">
<button class="prev" @click="prev">Previous</button> 
<button class="play" v-if="!isPlaying" @click="play(songs[0])">Play</button> 
<button class="pause" v-else @click="pause">Pause</button>  
<button class="next" @click="next">Next</button>
     
</div>
</section>
<section class="playlist">
<h3>The PlayList</h3>
<button v-for="song in songs" :key="song.id" @click="play(song)" :class="(song.src == current.src)? 'playing' :'song'">{{song.title}} -{{song.artist}}</button>
</section>
</main>
</div>
</template>

<script>
export default {
    name: 'App',
    data(){
      return {
        current:{},
        index: 0,
        isPlaying: false,
        songs: [
          
          {
            title : 'Faded',
            artist : 'Alan Walker',
            src: require('./assets/faded.mp3'),
            id: 32879278972474217889248092890
            
          },
          {
            title : 'Alone',
            artist : 'Alan Walker',
            id:72177021771478471664674,
            src: require('./assets/Alone.mp3')
          },
          {
          title : 'Let me Love you',
          artist: 'Justin Bieber',
          src: require('./assets/let_me_love_you.mp3'),
          id: 731738791341979858158580158
          }

        ],
        player: new Audio(),
      }
    },
    methods:{
      play(song){
        if(typeof song.src != undefined){
          this.current= song;
          this.player.src= this.current.src;

         
        }
        this.player.play();
        this.isPlaying= true;

        this.player.addEventListener('end',function(){
        this.index++;
        if(this.index > this.songs.length -1){
        this.index=0;
        }
        this.current= this.songs[this.index];
        this.play(this.current);
      }.bind(this))
        
      },
      pause(){
        this.isPlaying= false;
        this.player.pause();
      },
      prev(){
      this.index--;
      if(this.index<0){
          this.index = this.songs.length-1;
        }
        this.current= this.songs[this.index];
        this.play(this.current);
      
      },
      next(){
        this.index++;
        if(this.index > this.songs.length -1){
          this.index=0;
        }
        this.current= this.songs[this.index];
        this.play(this.current);
      }
    },
      created(){
          console.log("Created");
          this.current= this.songs[this.index];
          this.player.src= this.current.src;
          // this.player.play();
        }

      }
      
    


</script>

<style>
*{
  margin:0;
  padding:0;
  box-sizing: border-box;

}
body{
  font-family: sans-serif;
}
header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #FFF;
}
main{
  width:100%;
  margin:0 auto;
  max-width: 768px;
  padding:25px;
}
.song-title {
  color: #53565A;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}
.song-title span {
  font-weight: 400;
  font-style: italic;
}
.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}
button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}
button:hover {
  opacity: 0.8;
}
.play, .pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #FFF;
  background-color: #CC2E5D;
}
.next, .prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #FFF;
  background-color: #FF5858;
}
.playlist {
  padding: 0px 30px;
}
.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}
.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}
.playlist .song:hover {
  color: #FF5858;
}
.playlist .playing {
  margin-left: 35%;
  margin-bottom: 5%;
  padding: 20px;
  color: #FFF;
  background-image: linear-gradient(to right, #CC2E5D, #FF5858);
}
</style>

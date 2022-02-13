<template>
<div id="album">
  <div class="userBox">
    <div v-for="album in userAlbums" :key="album.id" class="eachUser"><br>
        <h1 class="al_box">Album</h1>
        <h2>{{ album.title }}</h2>
        <div class="showPicture"><button v-on:click="showImage(album.id)" class="showButton">Show Picture</button></div>
          <div v-bind:id="'A' + album.id" style="display: none;" class="image_grind"><span v-on:click="showImage(album.id)">X</span>

          <div v-for="img in album.album_photos" :key="img" class="pictureBox">
            <img v-bind:src="img" class="imageStyle">
          </div> 
        </div>   
    </div>  
    <router-view/>
  </div>
</div>  
</template>

<script>

export default {
  name: 'About',
  methods: {
    showImage: function(key){
     
      key = "A" + key;
      if(document.getElementById(key).style.display == "none"){document.getElementById(key).style.display = "grid";} 
      else{document.getElementById(key).style.display = "none";}
      
      }      
  },
  data() {
    var albums = this.$route.params.id
    let userAlbums = [];
    

fetch('https://jsonplaceholder.typicode.com/albums')
  .then(response => response.json())
  .then(json => {
      for(let i = 0; i <= json.length - 1; i++){
        let photos = [];
        if(json[i].userId == albums){
          fetch('https://jsonplaceholder.typicode.com/photos')
          .then(response => response.json())
          .then(photo_in => {
            for(let j = 0; j <= photo_in.length - 1; j++){
              if(photo_in[j].albumId == json[i].id){
                photos.push(photo_in[j].url);
              }
            }
          });
          let new_album = {id: json[i].id, title: json[i].title, album_photos: photos};
          userAlbums.push(new_album);          
        }
        
      }
  });
  console.log(userAlbums);
  return{userAlbums, albums}
  }
}


 
</script>

  

<style>
span{
    position: fixed;
    right: 50px;
    top: 50px;
    font-size: 50px;
    cursor: pointer;
}
  

  

.al_box{
  padding: 7px;
    border: 1px solid black;
    width: 25%;
    margin: auto;
}

.image_grind{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
    position: fixed;
    z-index: 10000;
    padding-top: 100px;
    left: 0px;
    top: 0px;
    height: 100%;
    width: 100%;
    overflow: auto;
    background: lightgrey;
    opacity: 85%;
}


.imageBox{
  display: none;
}

.showButton{
  margin: auto;
}

.imageStyle{
  width: 100px;
  height: 100px;

}

.showPicture{
  text-align: center;
  padding: 10px;
}

.titleH {
  text-align: center;
}

.lineA {
  height: 5px;
  background: #ec4148;
  width: 90%;
  margin: auto;
}

.wrapper {
  width: 90%;
  background: lightgrey;
  margin: 20px auto;
  border-radius: 15px;
  padding: 10px;
}

.greetings {
  text-align: center;
}
.userBox {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-row-gap: 15px;
  grid-column-gap: 15px;
  margin: 20px auto;
  padding: 10px;
}

.eachUser {
  box-shadow: 0 4px 8px 0 rgb(0 0 0 / 20%), 0 6px 20px 0 rgb(0 0 0 / 19%);
  margin: auto;
  width: 95%;
  height: 100%;
  background: #ec4148;
  color: white;
  text-align: center;
  margin: 15px;
  margin-left: auto;
  margin-right: auto;
}

.eachUser button {
  padding: 10px;
  border-radius: 10px;
  color: white;
  background: #f3ad21;
}

@media only screen and (max-width: 750px){
      .userBox {
      display: grid;
      grid-template-columns: auto;
      grid-row-gap: 15px;
      grid-column-gap: 15px;
      margin: 20px auto;
      padding: 10px;
    }

    .image_grind{
      display: grid;
      grid-template-columns: 1fr 1fr;
        position: fixed;
        z-index: 10000;
        padding-top: 100px;
        left: 0px;
        top: 0px;
        height: 100%;
        width: 100%;
        overflow: auto;
        background: lightgrey;
        opacity: 85%;

    }
}
</style>

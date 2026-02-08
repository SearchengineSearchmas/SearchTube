<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>SearchTube</title>

<style>
body{
  margin:0;
  background:#181818;
  font-family:Arial;
  color:white;
}

header{
  background:#ff0000;
  padding:10px 15px;
  font-size:22px;
}

#searchBar{
  width:96%;
  margin:10px auto;
  display:block;
  padding:8px;
  font-size:16px;
  border:none;
  outline:none;
  border-radius:5px;
}

#player{
  width:100%;
  padding:15px;
  box-sizing:border-box;
}

video{
  width:100%;
  background:black;
  max-height:60vh;
}

#feed{
  display:flex;
  flex-wrap:wrap;
  padding:10px;
  gap:10px;
}

.videoCard{
  width:calc(25% - 10px);
  background:#111;
  padding:8px;
  cursor:pointer;
  border-radius:6px;
}

.videoCard:hover{
  background:#222;
}

.thumb{
  width:100%;
  height:140px;
  background:#000;
  margin-bottom:5px;
  object-fit:cover;
}

.title{
  font-size:14px;
  font-weight:bold;
}

@media(max-width:900px){
  .videoCard{ width:calc(33.33% - 10px); }
}

@media(max-width:600px){
  .videoCard{ width:calc(50% - 10px); }
}
</style>
</head>

<body>

<header>SearchTube</header>

<input id="searchBar" placeholder="Search videos..." onkeyup="searchVideos()">

<div id="feed">

  <div class="videoCard" data-title="Big Buck Bunny" data-url="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4">
    <video class="thumb" muted loop></video>
    <div class="title">Big Buck Bunny</div>
  </div>

  <div class="videoCard" data-title="Elephants Dream" data-url="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ElephantsDream.mp4">
    <video class="thumb" muted loop></video>
    <div class="title">Elephants Dream</div>
  </div>

  <div class="videoCard" data-title="Sintel" data-url="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/Sintel.mp4">
    <video class="thumb" muted loop></video>
    <div class="title">Sintel</div>
  </div>

  <div class="videoCard" data-title="Tears of Steel" data-url="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/TearsOfSteel.mp4">
    <video class="thumb" muted loop></video>
    <div class="title">Tears of Steel</div>
  </div>

  <div class="videoCard" data-title="For Bigger Blazes" data-url="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerBlazes.mp4">
    <video class="thumb" muted loop></video>
    <div class="title">For Bigger Blazes</div>
  </div>

</div>

<script>
var cards = document.getElementsByClassName("videoCard");

for(var i=0;i<cards.length;i++){
  (function(card){
    var url = card.getAttribute("data-url");
    var v = card.getElementsByTagName("video")[0];

    v.src = url;
    v.onloadeddata = function(){
      v.currentTime = 5;
      v.play();
    };

    card.onclick = function(){
      playVideo(url, card.getAttribute("data-title"));
    };
  })(cards[i]);
}

function playVideo(url,title){
  var video = document.getElementById("mainVideo");
  var src = document.getElementById("videoSrc");
  var text = document.getElementById("videoTitle");

  src.src = url;
  video.load();
  video.play();
  text.innerHTML = title;
}

function searchVideos(){
  var q = document.getElementById("searchBar").value.toLowerCase();

  for(var i=0;i<cards.length;i++){
    var title = cards[i].getAttribute("data-title").toLowerCase();
    cards[i].style.display = title.indexOf(q) > -1 ? "" : "none";
  }
}
</script>

</body>
</html>

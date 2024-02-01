# In index.html:
```
<html><head><link href="https://cdn.jsdelivr.net/npm/daisyui@3.1.6/dist/full.css" rel="stylesheet" type="text/css" /><script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script><script src="https://cdn.tailwindcss.com?plugins=forms,typography,aspect-ratio"></script><script defer src="https://cdnjs.cloudflare.com/ajax/libs/three.js/0.156.1/three.min.js"></script><script type="module" src="main.js"></script><title>REM Music</title></head><body><header><h1>REM</h1></header><main id="main"></main><nav id="sidebar"><ol id="nav"><li><a href="/" style="font-size: 18px;">Home</a></li><li><a href="/top50" style="font-size: 18px;">Top 50</a></li><li><a href="/albums" style="font-size: 18px;">Albums</a></li></ol></nav></body></html>
```
# In main.js:
```
// Include AlpineJS and DaisyUI
import { configure } from "https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js";
import "https://cdn.jsdelivr.net/npm/daisyui@3.1.6/dist/full.css";

// Import the stylesheet in the module
import { css } from "https://cdn.tailwindcss.com?plugins=forms,typography,aspect-ratio";

// Get the main element
const main = document.querySelector("#main");

// Add a music player component to the main element
main.innerHTML = `
 <nav>
    <ul>
      <li><a href="/song/yes-and">Yes and</a></li>
      <li><a href="/song/reputation">Reputation</a></li>
      <li><a href="/song/sour">Sour</a></li>
      <li><a href="/song/agua">Agua</a></li>
    </ul>
 </nav>
 <div id="player">
    <h1>REM</h1>
    <div class="song-info">
      <h2>Current Song</h2>
      <span class="song-title"></span>
      <span class="song-artist"></span>
    </div>
    <div class="progress-bar">
      <div class="progress-bar-fill" style="width: 0"></div>
      <div class="progress-bar-fill" style="width: 0"></div>
    </div>
 </div>
`;

// Create an array of songs to play
const songs = [
 {
    title: "Yes and",
    artist: "Ariana Grande",
    url: "/song/yes-and",
 },
 {
    title: "Reputation",
    artist: "Taylor Swift",
    url: "/song/reputation",
 },
 {
    title: "Sour",
    artist: "Chanel",
    url: "/song/sour",
 },
 {
    title: "Agua",
    artist: "Olivia Rodrigo",
    url: "/song/agua",
 },
];

// Set the current song and artist
main.querySelector(".song-title").textContent = songs[0].title;
main.querySelector(".song-artist").textContent = songs[0].artist;

// Set up the player
const player = main.querySelector("#player");
player.classList.add("is-playing");
const progressBar = player.querySelector(".progress-bar-fill");
const currentTime = player.querySelector(".player-current-time");
const duration = player.querySelector(".player-duration");
const time = player.querySelector(".player-width");
const volume = player.querySelector(".player-volume");
const currentSongIndex = main.querySelector(".song-title").textContent;

// Set up the player controls
document.querySelector(".player-prev").addEventListener("click", () => {
 player.classList.remove("is-playing");
 volume.value = 0;
 progressBar.style.width = "0";
 time.textContent = "0:00";
 duration.textContent = "0:00";
 currentTime.textContent = "0:00";
 player.classList.add("is-playing");
 volume.value = 1.0;
 progressBar.style.width = "100%";
 time.textContent = "0:00";
 duration.textContent = "0:00";
 currentTime.textContent = "0:00";
 player.classList.remove("is-playing");
 player.classList.add("is-paused");
});

document.querySelector(".player-next").addEventListener("click", () => {
 player.classList.remove("is-playing");
 volume.value = 0;
 progressBar.style.width = "0";
 time.textContent = "0:00";
 duration.textContent = "0:00";
 currentTime.textContent = "0:00";
 player.classList.add("is-playing");
 volume.value = 1.0;
 progressBar.style.width = "100%";
 time.textContent = "0:00";
 duration.textContent = "0:00";
 currentTime.textContent = "0:00";
 player.classList.remove("is-playing");
 player.classList.add("is-paused");
});

document.querySelector(".player-volume").addEventListener("click", () => {
 volume.value = 0;
});

document.querySelector(".player-volume").addEventListener("click", () => {
 volume.value = 1.0;
});

// Set up the song list
const songList = document.querySelector(".song-list");

songs.forEach((song, index) => {
 const li = document.createElement("li");
 li.innerHTML = `
    <a href="${song.url}">${song.title}</a>
 `;
 songList.appendChild(li);
});

// Set up the top 50 list
const top50List = document.querySelector(".top50-list");

const top50 = [
 {
    title: "Yes and",
    artist: "Ariana Grande",
    url: "/album/yes-and",
 },
 {
    title: "Reputation",
    artist: "Taylor Swift",
    url: "/album/reputation",
 },
 {
    title: "Sour",
    artist: "Chanel",
    url: "/album/sour",
 },
 {
    title: "Agua",
    artist: "Olivia Rodrigo",
    url: "/album/agua",
 },
];

top50.forEach((song, index) => {
 const li = document.createElement("li");
 li.innerHTML = `
    <a href="${song.url}">${song.title}</a>
 `;
 top50List.appendChild(li);
});

// Set up the sidebar
const sidebar = document.querySelector(".sidebar");

sidebar.addEventListener("click", (event) => {
 if (event.target.tagName === "A") {
    const url = event.target.getAttribute("href");
    openAnimalModal(url);
 }
});

const openAnimalModal = (url) => {
 const modal = document.createElement("div");
 modal.classList.add("modal");
 modal.innerHTML = `
    <div class="modal-inner">
      <div class="modal-content">
        <div class="promo-order">
          <a href="${url}">Order Now</a>
        </div>
        <div class="modal-close">
          <button>Close</button>
        </div>
      </div>
    </div>
 `;
 document.body.appendChild(modal);
 modal.style.display = "block";
};
```
# In style.css:
```
* {
 box-sizing: border-box;
}

body {
 font-family: Arial, sans-serif;
 margin: 0;
 padding: 0;
 background-color: #f0f0f0;
 display: flex;
 flex-direction: column;
 min-height: 100vh;
}

#main {
 padding: 20px;
}

.song-list {
 list-style: none;
 margin: 0;
 padding: 0;
}

.song-list li {
 background-color: #f0f0f0;
 padding: 10px;
 margin-bottom: 10px;
}

.song-list li a {
 text-decoration: none;
 color: inherit;
}

.song-list li:hover {
 background-color: #e0e0e0;
}

.album-list {
 list-style: none;
 margin: 0;
 padding: 0;
}

.album-list li {
 background-color: #f0f0f0;
 padding: 10px;
 margin-bottom: 10px;
}

.album-list li a {
 text-decoration: none;
 color: inherit;
}

.album-list li:hover {
 background-color: #e0e0e0;
}

.sidebar {
 background-color: #333;
 color: #fff;
 padding: 20px;
 width: 250px;
 height: 100%;
 position: fixed;
 top: 0;
 left: 0;
 box-sizing: border-box;
}

.sidebar a {
 color: #fff;
}

.modal {
 display: none;
 position: fixed;
 z-index: 1000;
 padding-top: 100px;
 left: 0;
 top: 0;
 width: 100%;
 height: 100%;
 overflow: auto;
 background-color: rgba(0, 0, 0, 0.5);
}

.modal .modal-inner {
 background-color: #fff;
 margin: auto;
 padding: 20px;
 border: 1px solid #888;
 width: 80%;
 position: relative;
}

.modal .modal-inner .modal-close {
 position: absolute;
 top: 20px;
 right: 30px;
 font-size: 30px;
 font-weight: bold;
 color: #333;
 cursor: pointer;
}
```
# In README.md:
```
---
license: apache-2.0
title: REM Music
sdk: static
emoji: 👨‍💻
colorFrom: yellow
colorTo: green
---

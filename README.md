<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>NEON ARCADE</title>
<style>
* { box-sizing: border-box; }
body {
margin: 0;
background: #090914;
color: white;
font-family: Arial, sans-serif;
}
header {
text-align: center;
padding: 35px 15px;
background: linear-gradient(120deg,#29105b,#101b45);
border-bottom: 2px solid #8b5cf6;
}
h1 { color: #bca5ff; letter-spacing: 4px; }
header p { color: #c9c4e7; }
input {
width: min(90%, 500px);
padding: 14px;
border-radius: 12px;
border: 1px solid #805cff;
background: #17172a;
color: white;
font-size: 16px;
}
nav {
display: flex;
flex-wrap: wrap;
justify-content: center;
gap: 10px;
padding: 20px;
}
button {
padding: 10px 16px;
border: 1px solid #7957ff;
border-radius: 20px;
color: white;
background: #21183c;
cursor: pointer;
}
button:hover { background: #6941d9; }
#games {
display: grid;
grid-template-columns: repeat(auto-fit,minmax(155px,1fr));
gap: 16px;
padding: 20px;
max-width: 1100px;
margin: auto;
}
.card {
display: block;
padding: 22px 14px;
min-height: 135px;
text-align: center;
background: linear-gradient(145deg,#1d1b36,#11111e);
border: 1px solid #393052;
border-radius: 16px;
text-decoration: none;
color: white;
transition: transform .2s,border-color .2s;
}
.card:hover {
transform: translateY(-4px);
border-color: #b49aff;
}
.emoji { font-size: 38px; display: block; margin-bottom: 12px; }
small { display: block; color: #b8b0d3; margin-top: 8px; }
footer { text-align: center; padding: 25px; color: #9992b5; }
</style>
</head>
<body>
<header>
<h1>NEON ARCADE</h1>
<p>Your next game is waiting.</p>
<input id="search" placeholder="🔎 Search games..."
oninput="filterGames()">
</header>

<nav>
<button onclick="showCategory('All')">All Games</button>
<button onclick="showCategory('Platformer')">Platformers</button>
<button onclick="showCategory('Horror')">Horror</button>
<button onclick="showCategory('Sandbox')">Sandbox</button>
<button onclick="showCategory('Indie')">Indie Games</button>
<button onclick="showCategory('Favorites')">★ Favorites</button>
</nav>

<main id="games"></main>

<footer>NEON ARCADE · Game responsibly</footer>

<script>
const games = [
{name:"OVO",cat:"Platformer",emoji:"🏃",url:"https://ovogame.com/&quot;},
{name:"Minecraft",cat:"Sandbox",emoji:"⛏️",url:"https://www.minecraft.net/&quot;},
{name:"Roblox",cat:"Sandbox",emoji:"🎮",url:"https://www.roblox.com/&quot;},
{name:"Fortnite",cat:"Action",emoji:"🎯",url:"https://www.fortnite.com/&quot;},
{name:"FNAF",cat:"Horror",emoji:"🐻",url:"https://store.steampowered.com/search/?term=Five+Nights+at+Freddys&quot;},
{name:"FNAF 2",cat:"Horror",emoji:"🎭",url:"https://store.steampowered.com/search/?term=FNAF+2&quot;},
{name:"FNAF 3",cat:"Horror",emoji:"🐰",url:"https://store.steampowered.com/search/?term=FNAF+3&quot;},
{name:"FNAF 4",cat:"Horror",emoji:"🌙",url:"https://store.steampowered.com/search/?term=FNAF+4&quot;},
{name:"Undertale",cat:"Indie",emoji:"❤️",url:"https://undertale.com/&quot;},
{name:"Celeste",cat:"Indie",emoji:"🏔️",url:"https://store.steampowered.com/app/504230/Celeste/&quot;},
{name:"Balatro",cat:"Indie",emoji:"🃏",url:"https://store.steampowered.com/app/2379780/Balatro/&quot;},
{name:"Geometry Dash",cat:"Platformer",emoji:"🟪",url:"https://www.robtopgames.com/&quot;},
{name:"Slither.io",cat:"Indie",emoji:"🐍",url:"https://slither.io/&quot;},
{name:"Little Nightmares",cat:"Horror",emoji:"👁️",url:"https://store.steampowered.com/search/?term=Little+Nightmares&quot;}
];

let category = "All";
let favorites = [];

function render(list) {
document.getElementById("games").innerHTML = list.map(g => `
<a class="card" href="${g.url}" target="_blank"
rel="noopener noreferrer">
<span class="emoji">${g.emoji}</span>
<strong>${g.name}</strong>
<small>${g.cat} · Open game ↗</small>
<button type="button" onclick="toggleFavorite(event,'${g.name}')">
${favorites.includes(g.name) ? "★ Saved" : "☆ Favorite"}
</button>
</a>
`).join("");
}

function filterGames() {
const query = document.getElementById("search").value.toLowerCase();
render(games.filter(g =>
(category === "All" || g.cat === category ||
(category === "Favorites" && favorites.includes(g.name))) &&
g.name.toLowerCase().includes(query)
));
}

function showCategory(cat) {
category = cat;
filterGames();
}

function toggleFavorite(event, name) {
event.preventDefault();
event.stopPropagation();
favorites = favorites.includes(name)
? favorites.filter(x => x !== name)
: [...favorites, name];
filterGames();
}

render(games);
</script>
</body>
</html>

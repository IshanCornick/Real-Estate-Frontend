
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Math Quiz Hub</title>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap" rel="stylesheet">
<style>
  body {
    background: #f5f5f5;
    color: #333;
    font-family: 'Roboto', sans-serif;
    text-align: center;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
.game-hub {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    padding: 20px;
    gap: 20px;
  }
.game-link, .sidebar {
    display: flex;
    flex-direction: column;
    align-items: center;
    border: 2px solid #004D40;
    border-radius: 10px;
    overflow: hidden;
    transition: transform 0.3s ease, border-color 0.3s ease;
    background: #FFFFFF;
    color: #004D40;
  }
.game-link:hover, .sidebar:hover {
    transform: translateY(-5px) scale(1.03);
    border-color: #00796B;
  }
img {
    max-width: 100%;
    height: auto;
    display: block;
  }
.game-name {
    color: #005B4F;
    font-size: 1.2em;
    margin: 10px 0;
    padding: 0 10px;
  }
 /* Sidebar CSS */
  .sidebar {
    position: fixed;
    left: 0;
    top: 10;
    width: 200px; /* Width of the sidebar */
    height: 50%;
    background: #E0F2F1; /* Sidebar background color */
    padding: 20px;
    box-sizing: border-box;
  }
.sidebar a {
    color: #00695C; /* Link color */
    text-decoration: none;
    font-size: 16px;
    display: block;
    margin-bottom: 10px;
  }
.sidebar h2 {
    color: #004D40; /* Heading color */
    text-align: center;
    margin-bottom: 20px;
  }

</style>
</head>
<body>

<div class="sidebar">
  <h2>Menu</h2>
  <a href="https://spotify.com" target="_blank">Spotify</a>
  <a href="https://www.apple.com/apple-music/" target="_blank">Apple Music</a>
  <a href="https://soundcloud.com" target="_blank">SoundCloud</a>
  <a href="https://www.youtube.com" target="_blank">YouTube</a>
  <a href="https://www.deezer.com" target="_blank">Deezer</a>
</div>

<div class="game-hub">
   
<a href="http://127.0.0.1:4200/student/2024/02/15/studygame-calc.html" class="game-link">
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQzlURkQ6-4U8oI5Acrya2l8cFRqiPSOZtJFw&usqp=CAUr" alt="Studygame Calc">
    <div class="game-name">Calculus quiz maker</div>
  </a>
  <a href="http://127.0.0.1:4200/student/2024/02/16/gradelevel.html" class="game-link">
    <img src="" alt="Gradelevel">
    <div class="game-name">Gradelevel</div>
    <a>


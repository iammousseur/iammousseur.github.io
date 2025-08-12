<html lang="ru">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Мой сайт</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background-color: #222;
    color: #fff;
    margin: 0;
    padding: 0;
  }
  header {
    background-color: #111;
    padding: 10px;
    text-align: center;
    font-size: 24px;
  }
  .container {
    max-width: 900px;
    margin: 20px auto;
    background-color: #333;
    padding: 20px;
    border-radius: 8px;
  }
  .image-section {
    text-align: center;
    margin-bottom: 20px;
  }
  .image-section img {
    max-width: 250px;
    border: 2px solid #fff;
    border-radius: 4px;
  }
  .player-section {
    background-color: #444;
    padding: 10px;
    border-radius: 4px;
  }
  .song-info {
    margin-bottom: 10px;
  }
  audio {
    width: 100%;
  }
  .controls {
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-top: 10px;
  }
  .song-list {
    margin-top: 20px;
    background-color: #555;
    padding: 10px;
    border-radius: 4px;
    max-height: 200px;
    overflow-y: auto;
  }
  .song {
    padding: 5px 0;
    border-bottom: 1px solid #666;
  }
  .bottom {
    display: flex;
    justify-content: space-between;
    margin-top: 20px;
  }
  button {
    padding: 8px 16px;
    background-color: #777;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  button:hover {
    background-color: #999;
  }
  footer {
    text-align: center;
    padding: 10px;
    background-color: #111;
    margin-top: 20px;
  }
  /* Для выделения выбранной песни */
  .song.selected {
    background-color: #888;
  }
</style>
</head>
<body>

<header>
  Нарративффички
</header>

<div class="container">
  <!-- Изображение -->
  <div class="image-section">
    <img src="https://via.placeholder.com/250x250.png?text=Рамка" alt="Рамка" />
  </div>

  <!-- Плеер и информация -->
  <div class="player-section">
    <div class="song-info" id="current-song-title">Название песни: <span id="song-title">Песня 1</span></div>
    <div class="song-info" id="current-song-duration">Длительность: <span id="song-duration">3:45</span></div>
    <audio id="audio-player" src="https://www.w3schools.com/html/horse.mp3"></audio>
    <!-- Кнопки управления -->
    <div class="controls">
      <button id="playBtn">▶️ Воспроизвести</button>
      <button id="pauseBtn">⏸️ Пауза</button>
      <button id="stopBtn">⏹️ Стоп</button>
    </div>
  </div>

  <!-- Список песен -->
  <div class="song-list" id="songList">
    <div class="song selected" data-src="https://www.w3schools.com/html/horse.mp3" data-title="Песня 1" data-duration="3:45">1. Название песни 1 — 3:45</div>
    <div class="song" data-src="https://www.w3schools.com/html/horse.mp3" data-title="Песня 2" data-duration="4:10">2. Название песни 2 — 4:10</div>
    <div class="song" data-src="https://www.w3schools.com/html/horse.mp3" data-title="Песня 3" data-duration="2:50">3. Название песни 3 — 2:50</div>
    <div class="song" data-src="https://www.w3schools.com/html/horse.mp3" data-title="Песня 4" data-duration="3:20">4. Название песни 4 — 3:20</div>
    <div class="song" data-src="https://www.w3schools.com/html/horse.mp3" data-title="Песня 5" data-duration="4:00">5. Название песни 5 — 4:00</div>
  </div>

  <!-- Кнопки добавления и удаления -->
  <div class="bottom">
    <button id="addBtn">Добавить</button>
    <button id="deleteBtn">Удалить</button>
  </div>
</div>

<!-- Логотип в футере -->
<footer>
  <img src="https://via.placeholder.com/50x50.png?text=Лого" alt="Логотип" />
</footer>

<script>
  const audio = document.getElementById('audio-player');
  const playBtn = document.getElementById('playBtn');
  const pauseBtn = document.getElementById('pauseBtn');
  const stopBtn = document.getElementById('stopBtn');
  const songList = document.getElementById('songList');
  const songItems = songList.querySelectorAll('.song');

  const songTitle = document.getElementById('song-title');
  const songDuration = document.getElementById('song-duration');

  let currentSongIndex = 0;

Сергей Николаевич, [12.08.2025 13:32]
// Обработка кнопок управления
  playBtn.onclick = () => { audio.play(); };
  pauseBtn.onclick = () => { audio.pause(); };
  stopBtn.onclick = () => { audio.pause(); audio.currentTime = 0; };

  // Обработка выбора песни из списка
  songItems.forEach((item, index) => {
    item.onclick = () => {
      // Убираем выделение у всех
      songItems.forEach(i => i.classList.remove('selected'));
      // Выделяем выбранную
      item.classList.add('selected');
      // Обновляем текущий трек
      const src = item.getAttribute('data-src');
      const title = item.getAttribute('data-title');
      const duration = item.getAttribute('data-duration');

      audio.src = src;
      songTitle.textContent = title;
      songDuration.textContent = duration;
      audio.play();
      currentSongIndex = index;
    };
  });

  // Кнопки "Добавить" и "Удалить"
  document.getElementById('addBtn').onclick = () => {
    const newIndex = songItems.length + 1;
    const newSong = document.createElement('div');
    newSong.className = 'song';
    newSong.setAttribute('data-src', 'https://www.w3schools.com/html/horse.mp3');
    newSong.setAttribute('data-title', 'Песня ' + newIndex);
    newSong.setAttribute('data-duration', '3:30');
    newSong.textContent = ${newIndex}. Название песни ${newIndex} — 3:30;
    // Добавляем обработчик клика
    newSong.onclick = () => {
      songItems.forEach(i => i.classList.remove('selected'));
      newSong.classList.add('selected');
      audio.src = newSong.getAttribute('data-src');
      songTitle.textContent = newSong.getAttribute('data-title');
      songDuration.textContent = newSong.getAttribute('data-duration');
      audio.play();
      currentSongIndex = Array.prototype.indexOf.call(songList.children, newSong);
    };
    songList.appendChild(newSong);
  };

  document.getElementById('deleteBtn').onclick = () => {
    if (songItems.length > 0) {
      const last = songItems[songItems.length - 1];
      if (last.classList.contains('selected')) {
        // Если удаляем выбранный, переключимся на первый
        audio.pause();
        if (songItems.length > 1) {
          songItems[0].classList.add('selected');
          audio.src = songItems[0].getAttribute('data-src');
          songTitle.textContent = songItems[0].getAttribute('data-title');
          songDuration.textContent = songItems[0].getAttribute('data-duration');
        } else {
          // Нет песен
          audio.src = '';
          songTitle.textContent = '';
          songDuration.textContent = '';
        }
      }
      last.remove();
    }
  };
</script>

</body>
</html>
